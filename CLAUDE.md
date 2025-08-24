# Todo App Project Configuration

## Project Overview
This is a modern Todo application built with:
- **Frontend**: React with React Router v7
- **Database**: SQLite
- **Testing**: Vitest for unit tests, Playwright for e2e tests
- **Deployment**: Cloudflare Workers

## Technology Stack Details

### Frontend Framework
- React with modern hooks and functional components
- React Router v7 for client-side routing
- TypeScript for type safety
- Modern CSS or styled-components for styling

### Database
- SQLite for local development
- Consider SQLite-compatible solutions for Cloudflare Workers (like D1)

### Testing
- **Unit Tests**: Vitest
  - Test React components with @testing-library/react
  - Mock API calls and database interactions
  - Aim for high coverage of business logic
- **E2E Tests**: Playwright
  - Test critical user flows (add/edit/delete todos)
  - Cross-browser testing
  - Mobile responsive testing

### Deployment
- **Platform**: Cloudflare Workers
- **Database**: Cloudflare D1 (SQLite-compatible)
- **Static Assets**: Cloudflare Pages or Workers Sites
- **Environment**: Serverless edge computing

## Development Commands
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run test` - Run unit tests with Vitest
- `npm run test:e2e` - Run Playwright tests
- `npm run deploy` - Deploy to Cloudflare Workers

## Code Style Guidelines
- Use functional components with hooks
- Prefer composition over inheritance
- Write tests for all business logic
- Use semantic HTML and accessible components
- Follow React best practices for state management

## Architecture Notes
- Keep components small and focused
- Separate business logic from UI components
- Use proper error boundaries
- Implement proper loading and error states
- Consider offline functionality with service workers
- Run typecheck and lint after completing tasks and be sure they ALWAYS pass.