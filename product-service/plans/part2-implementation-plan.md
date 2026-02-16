# Part 2 - Implementing REST APIs Plan

## Overview
This plan outlines the implementation of CRUD REST endpoints for a Product microservice using Spring Boot.

## Current Project Status
- **Project**: product-service
- **Group**: com.sliit
- **Java Version**: 21
- **Spring Boot Version**: 4.0.2
- **Dependencies**: Spring Web MVC, Spring Data JPA, H2 Database, H2 Console

## Implementation Steps

### Step 1: Create Product Entity
**File**: `src/main/java/com/sliit/product_service/entity/Product.java`

Create a JPA entity class with the following structure:

```
@Entity
@Table(name = "products")
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String name;
    
    @Column(nullable = false)
    private Double price;
    
    // Constructors, Getters, and Setters
}
```

**Fields**:
- `id` - Auto-generated primary key
- `name` - Product name (required)
- `price` - Product price (required)

---

### Step 2: Create ProductRepository Interface
**File**: `src/main/java/com/sliit/product_service/repository/ProductRepository.java`

Create a repository interface extending JpaRepository:

```
@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
}
```

This provides built-in methods:
- `save()` - Save/update entity
- `findAll()` - Get all entities
- `findById()` - Get entity by ID
- `deleteById()` - Delete entity by ID

---

### Step 3: Create ProductController
**File**: `src/main/java/com/sliit/product_service/controller/ProductController.java`

Create a REST controller with the following endpoints:

#### Endpoints to Implement:

| Method | Endpoint | Description | HTTP Status |
|--------|----------|-------------|-------------|
| POST | `/api/products` | Create a new product | 201 Created |
| GET | `/api/products` | Get all products | 200 OK |
| GET | `/api/products/{id}` | Get product by ID | 200 OK / 404 Not Found |
| DELETE | `/api/products/{id}` | Delete product by ID | 204 No Content / 404 Not Found |

#### Controller Structure:

```
@RestController
@RequestMapping("/api/products")
public class ProductController {
    
    @Autowired
    private ProductRepository productRepository;
    
    // POST - Create product
    @PostMapping
    public ResponseEntity<Product> createProduct(@RequestBody Product product) {
        Product savedProduct = productRepository.save(product);
        return new ResponseEntity<>(savedProduct, HttpStatus.CREATED);
    }
    
    // GET - Get all products
    @GetMapping
    public ResponseEntity<List<Product>> getAllProducts() {
        List<Product> products = productRepository.findAll();
        return new ResponseEntity<>(products, HttpStatus.OK);
    }
    
    // GET - Get product by ID
    @GetMapping("/{id}")
    public ResponseEntity<Product> getProductById(@PathVariable Long id) {
        Optional<Product> product = productRepository.findById(id);
        return product.map(p -> new ResponseEntity<>(p, HttpStatus.OK))
                      .orElse(new ResponseEntity<>(HttpStatus.NOT_FOUND));
    }
    
    // DELETE - Delete product by ID
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteProduct(@PathVariable Long id) {
        if (productRepository.existsById(id)) {
            productRepository.deleteById(id);
            return new ResponseEntity<>(HttpStatus.NO_CONTENT);
        }
        return new ResponseEntity<>(HttpStatus.NOT_FOUND);
    }
}
```

---

## Project Structure After Implementation

```
src/main/java/com/sliit/product_service/
├── ProductServiceApplication.java
├── controller/
│   └── ProductController.java
├── entity/
│   └── Product.java
└── repository/
    └── ProductRepository.java
```

---

## Testing the APIs

Once implemented, you can test the endpoints using:

1. **curl commands**:
   ```bash
   # Create product
   curl -X POST http://localhost:8080/api/products -H "Content-Type: application/json" -d "{\"name\":\"Laptop\",\"price\":999.99}"
   
   # Get all products
   curl http://localhost:8080/api/products
   
   # Get product by ID
   curl http://localhost:8080/api/products/1
   
   # Delete product
   curl -X DELETE http://localhost:8080/api/products/1
   ```

2. **Postman** or similar API testing tools

3. **Swagger UI** (after Part 4): `http://localhost:8080/swagger-ui.html`

---

## Notes

- The H2 database configuration will be done in Part 3
- Swagger/OpenAPI documentation will be added in Part 4
- The current pom.xml already has all required dependencies for Part 2

---

## Next Steps After Part 2

1. **Part 3**: Configure H2 database properties in application.properties
2. **Part 4**: Add springdoc-openapi dependency and verify Swagger UI
