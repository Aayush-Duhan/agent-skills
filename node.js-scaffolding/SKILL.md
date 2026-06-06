---
name: node.js-scaffolding
description: Instructions and guidelines for scaffolding Node.js applications with proper structure, authentication, and error handling.
---
# Node.js Scaffolding Specialist

Guidelines and rules to follow when scaffolding a Node.js project or adding authentication.

## Scaffolding Process

When scaffolding a Node.js project, follow this order:
1. **Directory Structure**: Create all directory structures inside a `src/` directory, even if they are initially empty:
   - `src/controllers`
   - `src/services`
   - `src/models`
   - `src/routes`
   - `src/types`
   - `src/validators`
   - `src/config`
   - `src/middlewares`
   - `src/utils`
2. **Dependencies**: Run `npm install` to get the latest package versions. Do **NOT** fabricate or hardcode versions in `package.json`.
3. **Core Files**: Create the following files:
   - `errorHandler.middleware.ts` and `asyncHandler.middleware.ts` in the `src/middlewares/` folder.
   - `getEnv` utility
   - `env.config`
   - `http.config`
   - `bcrypt` utility
   - `app-error.ts`
   - `index.ts` (with a health API route)
   - `nodemon.json`
   - `tsconfig.json`
   - `tsup.config.ts` (add a build script in `package.json`: `"build": "tsup src/index.ts --format cjs --out-dir dist && cp ./package.json ./dist"`)
   - `.gitignore`

## Component Guidelines

### Error Handling (`app-error.ts` and Middlewares)
- **Base Error Class**: Include an `ErrorCodes` constant with:
  - `ERR_INTERNAL`
  - `ERR_BAD_REQUEST`
  - `ERR_UNAUTHORIZED`
  - `ERR_FORBIDDEN`
  - `ERR_NOT_FOUND`
- **Exceptions**: Implement `ErrorCodeType`, `AppError` base class, and exception classes:
  - `InternalServerException`
  - `NotFoundException`
  - `BadRequestException`
  - `UnauthorizedException`
- **Middlewares Placement**: Place `asyncHandler` and `errorHandler` in the `src/middlewares/` folder (named as `asyncHandler.middleware.ts` and `errorHandler.middleware.ts`), not in `utils/`.
- **Validation Errors**: Always include `ZodError` handling in the `errorHandler` middleware. Check if `error instanceof ZodError` and return a formatted response with the error code `ERR_Validation` using a `formatZodError` helper.

### Database Setup
- **Strict Separation**: Do **NOT** include database connection setup (e.g., `database.config`, `connectDatabase` in `index.ts`, `MONGO_URI` in `env.config` or `.env`) in the initial scaffold. Only configure MongoDB/mongoose when explicitly requested to *"configure database mongodb"*.

### Verification
- **Runtime Check**: After setting up the Node.js project, always start the server (e.g., `npm run dev`) to verify it runs, rather than only running static checks like `tsc --noEmit`.

---

## Authentication Configuration

When adding authentication to a Node.js project, use the JWT strategy with `passport-jwt` + `jsonwebtoken` (do **NOT** use `passport-local` + `express-session`).

### Setup Steps
1. **Install Dependencies**: Install `passport`, `passport-jwt`, `jsonwebtoken` and their corresponding `@types/` packages.
2. **Extraction**: Extract JWT from cookies (`req.cookies.accessToken`) using `ExtractJwt.fromExtractors`.
3. **Core Files**:
   - `passport.config` with `JwtStrategy` configuration.
   - `cookie.ts` with `setJwtAuthCookie` / `clearJwtAuthCookie` helpers.
   - Passport initialization in `index.ts`.
   - User model, `user.service.ts`, and `auth.service.ts`.
   - Auth controller with login, register, logout, and auth status endpoints.
   - `auth.route.ts` (and import routes in `index.ts`).
