/*
    Category table
*/
CREATE TABLE Category (
    category_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    Name        varchar(255)    NOT NULL,
    Description    varchar(255)
);
/* Product table
-----
*/
CREATE TABLE Product (
    product_id    INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name        varchar(255) NOT NULL,
    SKU            varchar(255) UNIQUE NOT NULL, 
    total_quantity    int DEFAULT 0,
	is_active	BOOLEAN DEFAULT TRUE, 
    category_id INT NOT NULL,
    CONSTRAINT fk_category
    FOREIGN KEY (category_id)
    REFERENCES    Category(category_id) ON DELETE RESTRICT
);

/* 
    StockMovement table - ledger
*/

CREATE TABLE Ledger (
    ledger_id    INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    prod_quantity    INT NOT NULL,
    reason varchar(255) NOT NULL,
    date DATE NOT NULL,
    product_id INT NOT NULL,
    CONSTRAINT valid_reason CHECK (reason IN ('sold','restock','adjustment')),
    CONSTRAINT fk_product
    FOREIGN KEY (product_id)
    REFERENCES Product(product_id) ON DELETE RESTRICT

);