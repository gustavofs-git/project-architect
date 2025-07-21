# Setup Complete Project Architecture

## Feature: $ARGUMENTS

Generate complete project setup including CLAUDE.md files, project planning document, and individual PRPs for each feature. This command analyzes the project requirements and creates a comprehensive development environment with everything needed to implement the project from start to finish.

## Command Usage Examples

```
/setup-project-claude portifolio simples com hero, about me, contact form, services, projetos YouTube, PT-BR/EN, usando componentes liquid-glass
/setup-project-claude e-commerce com produtos, carrinho, checkout, pagamentos, admin panel, usando React e Python
/setup-project-claude app mobile fitness tracker com exercicios, progresso, social features, usando Flutter
/setup-project-claude SaaS dashboard com auth, analytics, billing, notifications, usando Next.js e Node.js
/setup-project-claude blog pessoal com posts, comments, newsletter, SEO, usando Astro e headless CMS
```

## Process Flow

### 1. Project Analysis and Information Gathering
- **Parse the project description** to identify:
  - Project type and purpose (portfolio, e-commerce, SaaS, mobile app, etc.)
  - Key features and sections needed
  - Technology preferences mentioned
  - Design requirements and references
  - Target audience and languages

- **Ask clarifying questions** to complete understanding:
  - "What technologies do you prefer? (React/Vue/Next.js for frontend, Python/Node.js for backend)"
  - "Do you need a database? Which one? (PostgreSQL, MongoDB, etc.)"
  - "Where will you deploy? (Vercel, Netlify, AWS, etc.)"
  - "Do you need authentication/user management?"
  - "Any specific design system or component library?"
  - "What's your timeline and complexity level?"

### 2. Feature Breakdown and Architecture Design
- **Break down the project** into individual features/components
- **Determine project architecture**:
  - Frontend-only, fullstack, or mobile
  - Monolith vs microservices
  - Database requirements
  - External integrations needed
- **Create feature list** for PRP generation

### 3. Planning Document Creation
- **Generate comprehensive project planning** document:
  - Project overview and objectives
  - Architecture diagrams and decisions
  - Technology stack rationale
  - Feature breakdown with priorities
  - Implementation timeline
  - Risk assessment and mitigation
  - Success criteria and metrics

### 4. Technology Research and Best Practices
- **Gather best practices** for chosen technology stack
- **Reference existing templates** from `claude_md_files/` directory
- **Include version-specific guidelines** and modern patterns
- **Add security considerations** and performance tips
- **Include testing strategies** for each technology

### 5. CLAUDE.md Generation Strategy

#### For Fullstack Projects:
```
project/
├── CLAUDE.md              # Project orchestrator & architecture
├── frontend/
│   └── CLAUDE.md          # Frontend-specific guidelines
├── backend/
│   └── CLAUDE.md          # Backend-specific guidelines
└── PRPs/                  # PRP infrastructure
    ├── templates/
    └── scripts/
```

#### For Monolith Projects:
```
project/
├── CLAUDE.md              # Single comprehensive file
└── PRPs/                  # PRP infrastructure
    ├── templates/
    └── scripts/
```

#### For Microservices:
```
project/
├── CLAUDE.md              # Overall architecture
├── services/
│   ├── user-service/
│   │   └── CLAUDE.md      # Service-specific guidelines
│   ├── product-service/
│   │   └── CLAUDE.md      # Service-specific guidelines
│   └── gateway/
│       └── CLAUDE.md      # Gateway-specific guidelines
└── PRPs/
```

### 6. Individual PRP Generation
- **Create separate PRPs** for each major feature identified:
  - Each PRP follows the standard template structure
  - Includes specific context for that feature
  - References relevant documentation and examples
  - Contains validation gates specific to the feature
  - Provides implementation blueprint with tasks

**Example PRPs for a portfolio project:**
- `PRPs/planning-portfolio.md` - Overall project planning
- `PRPs/hero-section.md` - Landing page hero implementation
- `PRPs/about-section.md` - About me section with content
- `PRPs/contact-form.md` - Contact form with validation
- `PRPs/services-section.md` - Services showcase
- `PRPs/projects-gallery.md` - YouTube projects integration
- `PRPs/internationalization.md` - Multi-language support
- `PRPs/database-setup.md` - Database schema and setup
- `PRPs/api-backend.md` - Backend API implementation
- `PRPs/deployment-setup.md` - Production deployment

### 7. Content Generation Rules

#### Root CLAUDE.md (Project Orchestrator)
Include:
- **Project Overview**: Architecture description and component relationships
- **Development Workflow**: How to run the full project (docker-compose, scripts)
- **Communication Patterns**: How components interact (APIs, message queues)
- **Deployment Strategy**: Production deployment guidelines
- **Environment Setup**: Prerequisites and initial setup steps
- **Testing Strategy**: Integration and E2E testing approaches
- **Security Guidelines**: Cross-cutting security concerns
- **Performance Considerations**: Optimization strategies

#### Frontend CLAUDE.md
Include technology-specific sections:
- **Component Architecture**: File organization and component patterns
- **State Management**: Redux, Context, Zustand patterns
- **Styling Guidelines**: CSS-in-JS, Tailwind, styled-components
- **API Integration**: HTTP clients, error handling, caching
- **Build & Bundle**: Webpack, Vite, optimization strategies
- **Testing**: Unit tests (Jest), integration tests, E2E tests
- **Accessibility**: WCAG guidelines and best practices
- **Performance**: Code splitting, lazy loading, metrics

#### Backend CLAUDE.md
Include technology-specific sections:
- **API Design**: REST patterns, GraphQL schemas, OpenAPI specs
- **Database Patterns**: ORM usage, migrations, query optimization
- **Authentication**: JWT, OAuth, session management
- **Error Handling**: Exception patterns, logging, monitoring
- **Validation**: Request/response validation patterns
- **Testing**: Unit tests, integration tests, test databases
- **Security**: Input sanitization, CORS, rate limiting
- **Performance**: Caching, database optimization, async patterns

### 8. Best Practices Integration

#### Python/FastAPI Backend:
- **Project Structure**: src/ layout, dependency injection patterns
- **Database**: SQLAlchemy patterns, Alembic migrations
- **API Design**: Pydantic models, dependency injection, middleware
- **Testing**: pytest patterns, fixtures, async testing
- **Code Quality**: ruff, mypy, pre-commit hooks
- **Documentation**: OpenAPI integration, docstrings

#### React Frontend:
- **Component Patterns**: Functional components, custom hooks, composition
- **TypeScript Integration**: Strict typing, utility types, generics
- **State Management**: Context vs external libraries decision matrix
- **Build Tools**: Vite configuration, environment variables
- **Code Quality**: ESLint, Prettier, Husky hooks
- **Bundle Optimization**: Code splitting, tree shaking, chunk strategies

#### Database Integration:
- **PostgreSQL**: Connection pooling, indexing strategies, migrations
- **MongoDB**: Schema design, aggregation patterns, indexing
- **Redis**: Caching patterns, session storage, pub/sub

### 9. Execute-All Command Generation
- **Create companion command** `/execute-all-prps-[project-name]` that:
  - Lists all generated PRPs in logical execution order
  - Provides option to execute all sequentially
  - Includes progress tracking and error handling
  - Allows selective execution of specific PRPs
  - Shows estimated time and complexity for each PRP

### 10. PRPs Directory Setup and Organization
- **Copy templates** from PRPs/templates/ if not present
- **Copy runner script** from PRPs/scripts/ if not present  
- **Create organized folder structure** for PRPs:
  ```
  PRPs/
  ├── [project-name]-planning.md
  ├── [project-name]-hero.md
  ├── [project-name]-about.md
  ├── [project-name]-contact.md
  ├── [project-name]-services.md
  ├── [project-name]-projects.md
  ├── [project-name]-i18n.md
  ├── [project-name]-database.md
  ├── [project-name]-api.md
  └── [project-name]-deployment.md
  ```

### 11. Validation and Quality Checks
- **Verify all CLAUDE.md files** have required sections
- **Check consistency** between planning and individual PRPs
- **Validate command examples** are executable
- **Ensure PRPs reference each other** appropriately
- **Test that execute-all command** works correctly

## Implementation Guidelines

### Command Execution Steps:
1. **Parse project description** and extract key requirements
2. **Ask clarifying questions** to complete understanding
3. **Create project planning** document with architecture decisions
4. **Break down project** into individual features/components
5. **Research best practices** for chosen technology stack
6. **Generate appropriate folder structure** and CLAUDE.md files
7. **Create individual PRPs** for each feature identified
8. **Generate execute-all command** for sequential PRP execution
9. **Validate all generated files** for consistency and completeness
10. **Provide comprehensive summary** and next steps guide

### Error Handling:
- **Invalid technology combinations**: Provide suggestions
- **Existing CLAUDE.md files**: Ask before overwriting, offer merge option
- **Missing directory permissions**: Clear error messages
- **Unknown technologies**: Graceful fallback with research

### Output Format:
```
🚀 Project Architecture Generated Successfully!

📁 Files Created:
   ├── CLAUDE.md (Project orchestrator)
   ├── frontend/CLAUDE.md (React + Tailwind)
   ├── backend/CLAUDE.md (Python + FastAPI)
   └── PRPs/
       ├── portfolio-planning.md
       ├── portfolio-hero.md
       ├── portfolio-about.md
       ├── portfolio-contact.md
       ├── portfolio-services.md
       ├── portfolio-projects.md
       ├── portfolio-i18n.md
       ├── portfolio-database.md
       ├── portfolio-api.md
       └── portfolio-deployment.md

🎯 Next Steps:
1. Review the planning document: PRPs/portfolio-planning.md
2. Execute PRPs individually: uv run PRPs/scripts/prp_runner.py --prp portfolio-hero --interactive
3. Or execute all at once: /execute-all-prps-portfolio
4. Customize CLAUDE.md files as needed for your specific requirements

⏱️ Estimated Implementation Time: 2-3 days
💡 Complexity Level: Medium
```

## Quality Standards

- **Comprehensive**: Cover all aspects of the technology stack
- **Current**: Use latest best practices and patterns
- **Consistent**: Ensure no conflicts between different CLAUDE.md files
- **Actionable**: Include specific commands and examples
- **Secure**: Include security best practices by default
- **Maintainable**: Structure that scales with project growth

## Success Criteria

- [ ] Generated CLAUDE.md files are technology-appropriate and comprehensive
- [ ] Planning document provides clear project roadmap and architecture
- [ ] Individual PRPs are feature-complete and executable
- [ ] All files work together without conflicts or contradictions
- [ ] Execute-all command works seamlessly for sequential execution
- [ ] Commands and examples in all files are executable
- [ ] Best practices are current and comprehensive
- [ ] User can immediately start implementing with generated setup
- [ ] Generated structure scales with project complexity
- [ ] Clear documentation and next steps provided

## Quality Standards

- **Comprehensive**: Each PRP contains all necessary context and implementation details
- **Consistent**: All generated files follow the same patterns and conventions
- **Current**: Uses latest best practices and modern development patterns
- **Executable**: Every command and example can be run immediately
- **Scalable**: Architecture supports future growth and modifications
- **Documented**: Clear explanations and rationale for all decisions

Remember: The goal is to provide a complete project setup that enables immediate productive development, from initial planning through final deployment.