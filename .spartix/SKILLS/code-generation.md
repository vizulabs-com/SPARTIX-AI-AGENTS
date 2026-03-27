# Skill: Code Generation

## Name
code-generation

## Version
1.0.0

## Description
Generate production-quality code in specified programming languages following project coding standards, design patterns, and architectural guidelines. This skill covers code creation for frontend, backend, mobile, desktop, CLI, blockchain, and infrastructure domains.

## Parameters
- **language**: Target programming language (e.g., TypeScript, Python, Rust, Solidity, Go)
- **framework**: Target framework if applicable (e.g., React, Django, Express, Next.js)
- **pattern**: Design pattern to follow (e.g., MVC, repository, factory, observer)
- **style_guide**: Project coding style guide reference
- **output_format**: File structure and naming convention requirements

## Outputs
- Generated source code files following project standards
- Inline documentation and code comments
- Import/dependency declarations

## Prerequisites
- Project coding standards must be defined in the active rule context
- Target language and framework must be specified in the task packet
- Architecture decisions must be documented in predecessor task outputs

## Approved Categories
- 04_FRONTEND_WEB_SPECIALISTS
- 05_BACKEND_AND_API_SPECIALISTS
- 06_DATABASE_AND_DATA_FOUNDATION
- 07_MOBILE_SPECIALISTS
- 08_DESKTOP_SPECIALISTS
- 17_WEB3_AND_BLOCKCHAIN
- 24_CLI_AND_DEVELOPER_TOOLING

## Usage Rules
- Generated code must pass all mandatory hooks including pre-action validation and post-action verification
- Code must follow the project's established patterns — never introduce new patterns without CO approval
- All generated code must include appropriate error handling, input validation, and logging
