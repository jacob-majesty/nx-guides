NX is a build system for monorepos, offering tools like dependency graphs and caching. A **monorepo** is a single repo with multiple projects, enabling code sharing and simplified dependencies. Benefits include atomic changes, centralized tooling, and easier CI/CD. Challenges are complexity, performance, and access control. NX simplifies monorepo management, optimizing builds and automating tasks.

---

# E-Commerce App with Angular, Spring Boot, and Nx

This guide explains how to set up a monorepo for an e-commerce application using **Angular** for the frontend, **Spring Boot** for the backend, and **Nx** for managing the monorepo. Nx allows you to manage both frontend and backend projects in a single workspace, making development and maintenance easier.

---

## **Prerequisites**
Before starting, ensure you have the following installed:
- **Node.js** (v16 or later)
- **npm** (comes with Node.js)
- **Java JDK** (v11 or later)
- **Maven** (for Spring Boot)
- **Angular CLI** (optional, but recommended)

---

## **Step 1: Create an Nx Workspace**
1. **Install Nx globally** (optional but recommended):
   ```bash
   npm install -g nx
   ```

2. **Create a new Nx workspace**:
   Run the following command to create a new Nx workspace for your e-commerce app:
   ```bash
   npx create-nx-workspace@latest ecom-app
   ```

3. **Follow the prompts**:
   - Choose **"Integrated"** or **"Preset"**.
   - Select **"Angular"** as the frontend framework.
   - Choose **"None"** for the backend framework (we'll add Spring Boot manually).

This will create a new Nx workspace named `ecom-app` with Angular configured.

---

## **Step 2: Add an Angular Frontend**
1. **Generate an Angular application**:
   Inside your Nx workspace, generate a new Angular app for the e-commerce frontend:
   ```bash
   nx generate @nrwl/angular:application frontend
   ```
   - Replace `frontend` with the name of your Angular app (e.g., `ecom-frontend`).

2. **Serve the Angular app**:
   Run the Angular app to verify it works:
   ```bash
   nx serve frontend
   ```
   Open your browser and navigate to `http://localhost:4200` to see the Angular app running.

---

## **Step 3: Add a Spring Boot Backend**
Nx does not natively support Spring Boot, but you can manually add a Spring Boot project to your workspace.

1. **Generate a Spring Boot project**:
   - Use [Spring Initializr](https://start.spring.io/) to generate a Spring Boot project.
   - Add dependencies like **Spring Web**, **Spring Data JPA**, and **H2 Database** for your e-commerce backend.
   - Download the project and extract it into the `apps` folder of your Nx workspace (e.g., `apps/backend`).

2. **Organize the Spring Boot project**:
   - Ensure the Spring Boot project is in the `apps/backend` folder.
   - Update the `pom.xml` or `build.gradle` file to match your workspace structure.

3. **Add Nx configuration for Spring Boot**:
   - Create a `project.json` file in the `apps/backend` folder to define Nx commands for Spring Boot:
     ```json
     {
       "targets": {
         "build": {
           "executor": "@nrwl/workspace:run-commands",
           "options": {
             "command": "./mvnw clean install",
             "cwd": "apps/backend"
           }
         },
         "serve": {
           "executor": "@nrwl/workspace:run-commands",
           "options": {
             "command": "./mvnw spring-boot:run",
             "cwd": "apps/backend"
           }
         }
       }
     }
     ```
   - This allows you to use Nx commands like `nx build backend` and `nx serve backend`.

4. **Run the Spring Boot app**:
   Start the Spring Boot backend:
   ```bash
   nx serve backend
   ```
   Verify the backend is running by visiting `http://localhost:8080`.

---

## **Step 4: Connect Angular and Spring Boot**
1. **Configure Angular to call the Spring Boot API**:
   - In your Angular app, update the `environment.ts` file to point to the Spring Boot backend:
     ```typescript
     export const environment = {
       production: false,
       apiUrl: 'http://localhost:8080/api'
     };
     ```

2. **Create Angular services**:
   - Use Angular's `HttpClient` to call the Spring Boot API. For example, create a service to fetch products:
     ```typescript
     import { HttpClient } from '@angular/common/http';
     import { Injectable } from '@angular/core';
     import { environment } from '../environments/environment';

     @Injectable({
       providedIn: 'root'
     })
     export class ProductService {
       private apiUrl = environment.apiUrl;

       constructor(private http: HttpClient) {}

       getProducts() {
         return this.http.get(`${this.apiUrl}/products`);
       }
     }
     ```

3. **Enable CORS in Spring Boot**:
   - Update your Spring Boot application to allow requests from the Angular app:
     ```java
     import org.springframework.context.annotation.Bean;
     import org.springframework.context.annotation.Configuration;
     import org.springframework.web.servlet.config.annotation.CorsRegistry;
     import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

     @Configuration
     public class CorsConfig {
         @Bean
         public WebMvcConfigurer corsConfigurer() {
             return new WebMvcConfigurer() {
                 @Override
                 public void addCorsMappings(CorsRegistry registry) {
                     registry.addMapping("/api/**")
                             .allowedOrigins("http://localhost:4200")
                             .allowedMethods("GET", "POST", "PUT", "DELETE");
                 }
             };
         }
     }
     ```

---

## **Step 5: Run Both Frontend and Backend**
1. **Run Angular**:
   ```bash
   nx serve frontend
   ```

2. **Run Spring Boot**:
   ```bash
   nx serve backend
   ```

3. **Test the integration**:
   - Open your Angular app at `http://localhost:4200`.
   - Ensure it can successfully call the Spring Boot API at `http://localhost:8080/api`.

---

## **Step 6: Build and Deploy**
1. **Build the Angular app**:
   ```bash
   nx build frontend
   ```

2. **Build the Spring Boot app**:
   ```bash
   nx build backend
   ```

3. **Deploy**:
   - Deploy the Spring Boot backend to a server (e.g., using Docker, Kubernetes, or a cloud provider).
   - Deploy the Angular app to a static hosting service (e.g., Netlify, Vercel, or AWS S3).

---

## **Optional: Use Nx Affected Commands**
Nx provides powerful tools for running commands only on affected projects. For example:
- Build only affected projects:
  ```bash
  nx affected:build
  ```
- Test only affected projects:
  ```bash
  nx affected:test
  ```

---

## **Folder Structure**
Your workspace should look like this:
```
ecom-app/
├── apps/
│   ├── frontend/       # Angular frontend
│   └── backend/        # Spring Boot backend
├── libs/               # Shared libraries (optional)
├── tools/              # Custom scripts and tools
├── nx.json             # Nx configuration
├── package.json        # Node.js dependencies
└── README.md           # Project documentation
```

---

## **Conclusion**
You now have a fully functional e-commerce app with Angular (frontend) and Spring Boot (backend) managed in a single Nx workspace. This setup allows for seamless development, testing, and deployment of both frontend and backend components.

For more information, refer to the official documentation:
- [Nx Documentation](https://nx.dev/)
- [Angular Documentation](https://angular.io/docs)
- [Spring Boot Documentation](https://spring.io/projects/spring-boot)

---

