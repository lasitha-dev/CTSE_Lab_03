# Part 3 - Using an In-Memory Database (H2) Plan

## Overview
Configure H2 in-memory database to persist data during runtime and enable the H2 console for database management.

## Current Status
- Part 2 completed: Product entity, repository, and controller are ready
- Current `application.properties` only contains: `spring.application.name=product-service`

---

## Implementation Steps

### Step 1: Configure H2 Database Properties

Add the following properties to `application.properties`:

```properties
# H2 Database Configuration
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# JPA/Hibernate Configuration
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
```

**Property Explanations:**

| Property | Description |
|----------|-------------|
| `spring.datasource.url` | H2 in-memory database URL. `mem:testdb` creates an in-memory database named `testdb` |
| `spring.datasource.driverClassName` | H2 JDBC driver class |
| `spring.datasource.username` | Default username for H2 is `sa` |
| `spring.datasource.password` | Default password is empty |
| `spring.jpa.hibernate.ddl-auto` | `create-drop` creates tables on startup and drops them on shutdown |
| `spring.jpa.show-sql` | Shows SQL queries in the console for debugging |

---

### Step 2: Enable H2 Console

Add the following properties to enable and configure the H2 console:

```properties
# H2 Console Configuration
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

**Property Explanations:**

| Property | Description |
|----------|-------------|
| `spring.h2.console.enabled` | Enables the H2 web console |
| `spring.h2.console.path` | URL path to access the console (default: `/h2-console`) |

---

### Complete application.properties

```properties
spring.application.name=product-service

# H2 Database Configuration
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# JPA/Hibernate Configuration
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true

# H2 Console Configuration
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

---

## Step 3: Run the Application

Run the Spring Boot application using one of these methods:

1. **Using Maven**:
   ```bash
   ./mvnw spring-boot:run
   ```

2. **Using IDE**: Run the `ProductServiceApplication` main class

---

## Step 4: Access H2 Console

1. Open browser and navigate to: `http://localhost:8080/h2-console`

2. Connect to the database using these settings:
   - **JDBC URL**: `jdbc:h2:mem:testdb`
   - **User Name**: `sa`
   - **Password**: (leave empty)

3. Click **Connect**

---

## Step 5: Verify Table Creation

Once connected to the H2 console, run the following SQL query to verify the `products` table was created:

```sql
SELECT * FROM products;
```

Or view the table structure:

```sql
DESCRIBE products;
```

**Expected Table Structure:**

| Column | Type | Constraints |
|--------|------|-------------|
| id | BIGINT | PRIMARY KEY, AUTO_INCREMENT |
| name | VARCHAR(255) | NOT NULL |
| price | DOUBLE | NOT NULL |

---

## Testing the APIs

After running the application, test the REST endpoints:

### 1. Create a Product (POST)
```bash
curl -X POST http://localhost:8080/api/products \
  -H "Content-Type: application/json" \
  -d "{\"name\":\"Laptop\",\"price\":999.99}"
```

### 2. Get All Products (GET)
```bash
curl http://localhost:8080/api/products
```

### 3. Get Product by ID (GET)
```bash
curl http://localhost:8080/api/products/1
```

### 4. Delete Product (DELETE)
```bash
curl -X DELETE http://localhost:8080/api/products/1
```

---

## Notes

- H2 in-memory database stores data in memory, so data is lost when the application restarts
- For persistent storage, change the URL to `jdbc:h2:file:./data/testdb`
- The `create-drop` DDL mode is suitable for development; use `update` or `validate` for production

---

## Next Steps

After completing Part 3:
- **Part 4**: Add springdoc-openapi dependency and enable Swagger UI documentation
