# Stage 1: Build Stage
FROM node:23 AS build

# Install pnpm globally
RUN corepack enable && corepack prepare pnpm@latest --activate

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and pnpm-lock.yaml to the working directory
COPY package.json pnpm-lock.yaml ./

# Install dependencies
RUN pnpm install

# Copy the rest of the application files
COPY . .

# Build the application
RUN pnpm run build


# Stage 2: Production Stage
FROM node:23-slim AS production

# Install pnpm globally
RUN corepack enable && corepack prepare pnpm@latest --activate

# Set the working directory
WORKDIR /usr/src/app

# Copy only the built application and required files from the build stage
COPY --from=build /usr/src/app/dist ./dist
COPY --from=build /usr/src/app/package.json /usr/src/app/pnpm-lock.yaml ./

# Install only production dependencies
RUN pnpm install --prod

# Expose the application port
EXPOSE 3000

# Command to run the application
CMD ["node", "dist/main"]
