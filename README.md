# DevOps Lab – 3  
**Building a Spring Boot Microservice with In-Memory Database & Swagger**

---

## Student Information
- **Name:** A.L.M Athulathmudali  
- **IT Number:** IT21129544  
- **Institution:** SLIIT   
- **Faculty:** Software Engineering  
- **Module:** Current Trends in Software Engineering (SE4010)  
- **Semester:** 1, 2026  

---

## 📌 Objective
Create a simple RESTful microservice using **Spring Boot**, integrate an **in-memory database (H2)**, and expose API documentation using **Swagger (OpenAPI)**.

---

## 🛠️ Part 1 – Creating a Spring Boot Microservice
1. Go to [Spring Initializr](https://start.spring.io)  
2. Project: **Maven** | Language: **Java** | Packaging: **Jar**  
3. Group: `com.sliit` | Artifact: `product-service`  
4. Add dependencies:
   - Spring Web  
   - Spring Data JPA  
   - H2 Database  
   - Springdoc OpenAPI UI  
5. Generate and open the project in your IDE  

---

## ⚙️ Part 2 – Implementing REST APIs
Create a **Product microservice** with CRUD REST endpoints.

- **Entity:** `Product` → fields: `id`, `name`, `price`  
- **Repository:** `ProductRepository` extending `JpaRepository`  
- **Controller:** `ProductController`  
- **Endpoints:**
  - `POST /products` → Add product  
  - `GET /products` → Get all products  
  - `GET /products/{id}` → Get product by ID  
  - `DELETE /products/{id}` → Delete product  

---

## 🗄️ Part 3 – Using an In-Memory Database (H2)
Use **H2 database** to persist data during runtime.

1. Configure H2 properties in `application.properties`  
2. Enable H2 console  
3. Run the application and access:
4. Verify table creation  

---

## 📖 Part 4 – Enabling Swagger (OpenAPI)
Expose API documentation using **Swagger UI**.

1. Add `springdoc-openapi` dependency  
2. Start the application  
3. Access Swagger UI:
4. Test APIs using Swagger UI  

---

## ✅ Expected Outcome
By completing this lab, students will be able to:
- Build a Spring Boot microservice with REST APIs  
- Use an in-memory database (H2)  
- Document APIs using Swagger UI  

---
