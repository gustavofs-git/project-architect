# Execute All PRPs in Sequence

## Project Name: $ARGUMENTS

Execute all PRPs created for a specific project in logical order with progress tracking and error handling.

## Command Usage Examples

```
/execute-all-prps portfolio
/execute-all-prps ecommerce
/execute-all-prps mobile-app
/execute-all-prps saas-dashboard
```

## Process Flow

### 1. PRP Discovery and Validation
- **Scan PRPs directory** for files matching the project pattern:
  - `PRPs/{project-name}-*.md`
  - Validate all referenced PRPs exist
  - Check for dependencies between PRPs

### 2. Execution Order Determination
- **Analyze PRPs** to determine logical execution sequence:
  - Planning documents first
  - Database/backend setup before frontend
  - Core features before advanced features
  - Deployment last

**Standard execution order:**
1. `{project}-planning.md` - Project planning and architecture
2. `{project}-database.md` - Database schema and setup
3. `{project}-api.md` - Backend API implementation
4. Core feature PRPs (hero, about, contact, etc.)
5. Advanced feature PRPs (i18n, analytics, etc.)
6. `{project}-deployment.md` - Production deployment

### 3. Interactive Execution Flow

#### Pre-Execution Summary
```
🎯 Found 10 PRPs for project: portfolio
📋 Execution Order:
   1. portfolio-planning.md (⏱️ ~30 min)
   2. portfolio-database.md (⏱️ ~20 min) 
   3. portfolio-api.md (⏱️ ~45 min)
   4. portfolio-hero.md (⏱️ ~25 min)
   5. portfolio-about.md (⏱️ ~15 min)
   6. portfolio-contact.md (⏱️ ~30 min)
   7. portfolio-services.md (⏱️ ~20 min)
   8. portfolio-projects.md (⏱️ ~35 min)
   9. portfolio-i18n.md (⏱️ ~40 min)
   10. portfolio-deployment.md (⏱️ ~25 min)

📊 Total estimated time: ~4.5 hours
⚙️ Execution modes available:
   [A] Execute all automatically
   [S] Execute step-by-step (pause between each)
   [C] Custom selection
   [Q] Quit

Choose mode [A/S/C/Q]: 
```

#### Step-by-Step Execution
```bash
# For each PRP in sequence:
echo "🚀 Executing PRP $CURRENT_INDEX/$TOTAL: $PRP_NAME"
echo "📝 Description: $PRP_DESCRIPTION"
echo "⏱️  Estimated time: $ESTIMATED_TIME"
echo ""
echo "Options:"
echo "  [E] Execute this PRP"
echo "  [S] Skip this PRP"
echo "  [V] View PRP details"
echo "  [Q] Quit execution"
echo ""
read -p "Choose action [E/S/V/Q]: " choice

case $choice in
    E|e)
        echo "▶️  Executing: $PRP_NAME"
        uv run PRPs/scripts/prp_runner.py --prp $(basename "$PRP_FILE" .md) --interactive
        
        if [ $? -eq 0 ]; then
            echo "✅ Completed: $PRP_NAME"
            COMPLETED_PRPS+=("$PRP_NAME")
        else
            echo "❌ Failed: $PRP_NAME"
            FAILED_PRPS+=("$PRP_NAME")
            echo "Continue with next PRP? [Y/N]: "
            read -p "" continue_choice
            [ "$continue_choice" != "Y" ] && [ "$continue_choice" != "y" ] && break
        fi
        ;;
    S|s)
        echo "⏭️  Skipped: $PRP_NAME"
        SKIPPED_PRPS+=("$PRP_NAME")
        ;;
    V|v)
        echo "📄 PRP Details:"
        head -20 "$PRP_FILE"
        echo "..."
        echo "Press enter to continue..."
        read
        # Re-show options for this PRP
        continue
        ;;
    Q|q)
        echo "🛑 Execution stopped by user"
        break
        ;;
esac
```

### 4. Automatic Execution Mode
```bash
# Execute all PRPs without interruption
for PRP_FILE in "${ORDERED_PRPS[@]}"; do
    PRP_NAME=$(basename "$PRP_FILE" .md)
    echo "🚀 Auto-executing: $PRP_NAME"
    
    # Execute with timeout and logging
    timeout 3600 uv run PRPs/scripts/prp_runner.py --prp "$PRP_NAME" --output-format stream-json 2>&1 | tee "logs/${PRP_NAME}-execution.log"
    
    if [ $? -eq 0 ]; then
        echo "✅ Completed: $PRP_NAME"
        COMPLETED_PRPS+=("$PRP_NAME")
    else
        echo "❌ Failed: $PRP_NAME"
        FAILED_PRPS+=("$PRP_NAME")
        
        # Auto mode: continue on failure but log it
        echo "⚠️  Continuing with next PRP..."
    fi
    
    # Brief pause between executions
    sleep 2
done
```

### 5. Custom Selection Mode
```bash
echo "📋 Available PRPs:"
for i in "${!ORDERED_PRPS[@]}"; do
    PRP_NAME=$(basename "${ORDERED_PRPS[$i]}" .md)
    echo "  [$((i+1))] $PRP_NAME"
done
echo ""
echo "Enter PRP numbers to execute (space-separated, e.g., '1 3 5'):"
echo "Or enter ranges (e.g., '1-3 7 9-10'):"
read -p "Selection: " selection

# Parse selection and execute chosen PRPs
parse_selection "$selection"
for selected_index in "${SELECTED_INDICES[@]}"; do
    execute_prp "${ORDERED_PRPS[$selected_index]}"
done
```

### 6. Progress Tracking and Logging

#### Real-time Progress Display
```
🎯 Project: portfolio | Mode: Step-by-Step
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40% (4/10)

📊 Status:
✅ Completed: planning, database, api, hero
🔄 Current: about (15 min remaining)
⏳ Pending: contact, services, projects, i18n, deployment

⏱️  Elapsed: 1h 45m | Remaining: ~2h 30m
💾 Logs: logs/portfolio-execution-2024-01-20.log
```

#### Execution Log Format
```
[2024-01-20 14:30:00] 🚀 Started execution: portfolio project
[2024-01-20 14:30:01] ▶️  Executing PRP 1/10: portfolio-planning
[2024-01-20 14:45:23] ✅ Completed PRP 1/10: portfolio-planning (15m 22s)
[2024-01-20 14:45:25] ▶️  Executing PRP 2/10: portfolio-database
[2024-01-20 15:02:17] ✅ Completed PRP 2/10: portfolio-database (16m 52s)
...
[2024-01-20 18:45:00] 🎉 All PRPs completed successfully!
[2024-01-20 18:45:00] 📊 Final Stats: 10 completed, 0 failed, 0 skipped
[2024-01-20 18:45:00] ⏱️  Total time: 4h 15m
```

### 7. Error Handling and Recovery

#### PRP Execution Failure
```bash
handle_prp_failure() {
    local prp_name=$1
    local error_code=$2
    
    echo "❌ PRP execution failed: $prp_name (exit code: $error_code)"
    echo ""
    echo "🔍 Possible actions:"
    echo "  [R] Retry this PRP"
    echo "  [S] Skip and continue"
    echo "  [V] View error details"
    echo "  [E] Edit PRP and retry"
    echo "  [Q] Quit execution"
    
    read -p "Choose action [R/S/V/E/Q]: " action
    
    case $action in
        R|r) execute_single_prp "$prp_name" ;;
        S|s) echo "⏭️  Skipping $prp_name"; return 0 ;;
        V|v) show_error_details "$prp_name"; handle_prp_failure "$prp_name" "$error_code" ;;
        E|e) open_prp_for_editing "$prp_name"; execute_single_prp "$prp_name" ;;
        Q|q) echo "🛑 Execution terminated"; exit 1 ;;
        *) echo "Invalid choice"; handle_prp_failure "$prp_name" "$error_code" ;;
    esac
}
```

### 8. Final Summary Report

```
🎉 Execution Complete: portfolio project

📊 Summary:
   ✅ Completed: 8 PRPs
   ❌ Failed: 1 PRP (portfolio-i18n)
   ⏭️  Skipped: 1 PRP (portfolio-deployment)
   
⏱️  Timing:
   Total time: 3h 42m
   Average per PRP: 22m
   
📁 Generated Files:
   - Frontend components: 12 files
   - Backend APIs: 8 endpoints
   - Database tables: 5 tables
   - Configuration files: 4 files
   
🔧 Next Steps:
   1. Review failed PRP: portfolio-i18n
   2. Test the implemented features
   3. Run final deployment when ready
   
📄 Full execution log: logs/portfolio-execution-2024-01-20.log
```

## Implementation Guidelines

### Command Execution Steps:
1. **Parse project name** from arguments
2. **Discover all PRPs** matching the project pattern
3. **Analyze dependencies** and determine execution order
4. **Present execution options** to user (auto/step/custom)
5. **Execute PRPs** according to chosen mode
6. **Track progress** and handle errors gracefully
7. **Generate final report** with results and next steps

### Error Handling:
- **Timeout protection**: Each PRP has execution timeout
- **Graceful failure**: Continue execution on non-critical failures
- **Recovery options**: Retry, skip, edit, or quit
- **Detailed logging**: Comprehensive logs for debugging
- **State preservation**: Track what's completed vs pending

### Integration Features:
- **Git integration**: Optional commits after each successful PRP
- **Backup creation**: Snapshot before each major PRP
- **Resource monitoring**: Track CPU/memory usage during execution
- **Notification support**: Alert when execution completes

## Quality Standards

- **Robust error handling**: Never crash, always provide recovery options
- **Clear progress indication**: Always show current status and remaining work
- **Flexible execution**: Support different execution modes for different use cases
- **Comprehensive logging**: Detailed logs for troubleshooting and auditing
- **User-friendly interface**: Intuitive prompts and clear feedback

Remember: The goal is to provide a seamless way to execute complex, multi-PRP projects while maintaining full visibility and control over the process.