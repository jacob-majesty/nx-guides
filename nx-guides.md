**Official Documentation:** https://nx.dev/

### Command Lines for project ecom-frontend

# Check out the Readme in workspace for additional commands for tasks

# Create te worspace
 npx create-nx-workspace

# Run the dev server
 npx nx serve ecom-frontend

# Set up tailwind css
 nx g @nx/angular:setup-tailwind ecom-frontend

# Set up daisy ui
 npm i -D daisyui@latest

# Set up tailwind typography
 https://github.com/tailwindlabs/tailwindcss-typography 

# Set up fortawesome icons for Angular
 npm install @fortawesome/free-solid-svg-icons @fortawesome/free-regular-svg-icons @fortawesome/free-brands-svg-icons
 npm install @fortawesome/angular-fontawesome

https://github.com/FortAwesome/angular-fontawesome/blob/main/docs/usage/using-other-styles.md 

# Create folder with various components
 nx g @nx/angular:component apps/ecom-frontend/src/app/layout/navbar/navbar
 nx g @nx/angular:component apps/ecom-frontend/src/app/layout/footer/footer

# Generating spring boot dependencies 
 npm install @nxrocks/nx-spring-boot --save-dev

 https://www.npmjs.com/package/@nxrocks/nx-spring-boot

# After, Go to Spring Initialzr to generate the project and configure project.json for integration Nx workspace









