---
name: assess
description: /assess
allowed-tools: Read
---

# /assess

Self-assess your knowledge in specific skills.

## Description

This command helps you evaluate your proficiency in specific developer skills and technologies. It provides:

- Self-assessment questionnaires
- Skill level ratings (Beginner → Intermediate → Advanced → Expert)
- Knowledge gap identification
- Personalized learning recommendations
- Progress tracking

## Usage

```
/assess
```

## What It Does

1. **Skill Selection** - Choose from 200+ skills organized by:
   - Programming languages
   - Frameworks and libraries
   - Tools and platforms
   - Architectural concepts
   - Specialized domains

2. **Assessment Quiz** - Answer 5-10 questions to evaluate:
   - Theoretical knowledge
   - Practical experience
   - Real-world application
   - Problem-solving ability
   - Best practices understanding

3. **Proficiency Report** - Get:
   - Current skill level
   - Detailed score breakdown
   - Strengths and weaknesses
   - Comparison to industry standards
   - Recommended learning paths

4. **Progress Tracking** - Monitor:
   - Skill improvements over time
   - Learning velocity
   - Completed milestones
   - Certification readiness

## Examples

### Example 1: Assess React Knowledge
```
> /assess
? Select skill category: Frontend Frameworks
? Select skill: React
▶ React Proficiency Assessment

Question 1/8: React Hooks Mastery
? Can you explain the dependency array in useEffect?
[Detailed explanation required]

Question 2/8: State Management
? How would you implement Redux with React?
...

═══════════════════════════════════════════
ASSESSMENT RESULTS
═══════════════════════════════════════════
Skill: React Development
Current Level: Intermediate (65/100)
Your Strengths:
  ✓ Component design
  ✓ State management basics
  ✓ React hooks
Your Gaps:
  ✗ Performance optimization
  ✗ Advanced patterns
  ✗ Testing strategies

Next Steps:
  → Learn: React.memo, useCallback, useMemo
  → Practice: Large-scale application architecture
  → Study: Advanced testing with React Testing Library
```

### Example 2: Assess Multiple Backend Skills
```
> /assess
? Assessment mode: Multiple skills
? Select skills: Python, Django, PostgreSQL, REST APIs
▶ Comprehensive Backend Assessment

Skills Assessed:
├── Python ................. Intermediate (72%)
├── Django ................. Intermediate (68%)
├── PostgreSQL ............. Beginner (45%)
└── REST API Design ........ Advanced (82%)

Overall Backend Score: 67/100 (Intermediate)

Career Path Recommendations:
  → Focus: Database design and optimization
  → Timeline: 2-3 months to reach Advanced level
  → Resources: PostgreSQL tutorials, query optimization
```

### Example 3: Track DevOps Skills Progress
```
> /assess
? Assessment mode: Progress tracking
? Role: DevOps Engineer
▶ Your DevOps Learning Progress

Completed Skills:
  ✓ Linux (Advanced)
  ✓ Docker (Intermediate)
  ✓ Git (Advanced)
  ✓ Bash Scripting (Intermediate)

In Progress:
  ▶ Kubernetes (30% complete)
  ▶ Terraform (40% complete)
  ▶ AWS (25% complete)

Not Started:
  ○ GCP
  ○ Azure
  ○ Prometheus & Monitoring

Estimated Time to DevOps Expert: 8-12 months
Current Velocity: 15% per month
```

## Assessment Features

### Skill Categories
- **Programming Languages** - JavaScript, Python, Java, Go, Rust, etc.
- **Frontend** - React, Vue, Angular, CSS, TypeScript, etc.
- **Backend** - Node.js, Django, Spring Boot, Express, etc.
- **Mobile** - Flutter, React Native, Swift, Kotlin, etc.
- **DevOps** - Docker, Kubernetes, Terraform, AWS, etc.
- **Data** - ML, Data Engineering, Analytics, etc.
- **Databases** - SQL, MongoDB, Redis, PostgreSQL, etc.
- **Architecture** - System Design, Design Patterns, etc.

### Question Types
- **Theoretical** - Explain concepts and best practices
- **Practical** - Solve real-world problems
- **Code Review** - Identify issues and improvements
- **Architecture** - Design system components
- **Decision Making** - Choose appropriate technologies

### Scoring Levels
- **Beginner** (0-35%) - Learning fundamentals
- **Intermediate** (36-70%) - Building production applications
- **Advanced** (71-90%) - Optimizing and architecting systems
- **Expert** (91-100%) - Teaching and mentoring others

## Learning Paths

After assessment, get personalized recommendations:
- Specific topics to study
- Recommended resources (tutorials, books, courses)
- Practice projects
- Timeline to next proficiency level
- Certification paths

## Related Commands

- `/learn` - Start a structured learning path
- `/explore` - Browse available roles and skills
- `/roadmap` - View detailed roadmap for a role

---

*Know your strengths, improve your weaknesses!*
