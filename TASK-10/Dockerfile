# ---------- Stage 1: Build ----------
FROM node:lts-alpine3.22 AS builder

# Set working directory
WORKDIR /app

# Copy dependency files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application files
COPY backend/ backend/

# ---------- Stage 2: Runtime ----------
FROM node:lts-alpine3.22

# Create app directory
WORKDIR /app

# Copy only necessary files from builder stage
COPY --from=builder /app /app

# Create non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Set ownership to appuser
RUN chown -R appuser:appgroup /app

# Switch to non-root user
USER appuser

# Expose port
EXPOSE 3000

# Start the app
CMD ["node", "backend/server.js"]
