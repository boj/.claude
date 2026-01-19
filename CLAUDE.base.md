# AI Rules - Universal

These rules apply to ALL roles and cannot be overridden.

## Safety
- NEVER log passwords or sensitive data
- NEVER send sensitive data over wire unless specifically required
- Always verify user ownership before allowing modifications
- NEVER access files outside project directory without asking

## File Handling
- Read before writing - understand existing code first
- Prefer editing existing files over creating new ones
- Don't create documentation files unless explicitly asked

## Deployment
- NEVER deploy directly from a developer machine
- ALWAYS follow the commit -> PR -> GitHub Actions deploy path
