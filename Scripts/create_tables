/*
===============================================================================
DDL Script: Create Bronze Tables
===============================================================================
Script Purpose:
    This script drops existing tables in the 'bronze' schema if they already exist 
    and recreates them. The Bronze layer serves as the raw data ingestion zone 
    where data from CRM and ERP source systems is loaded as-is without transformations.
===============================================================================
*/

-- ============================================================================
-- CRM Tables
-- ============================================================================

-- Drop and recreate customer information table from CRM source
IF OBJECT_ID('bronze.crm_cust_info', 'U') IS NOT NULL
	DROP TABLE bronze.crm_cust_info;
CREATE TABLE bronze.crm_cust_info (
    cst_id INT,                       -- Unique customer identifier
    cst_key NVARCHAR(50),             -- Business key / source system key
    cst_firstname NVARCHAR(50),       -- Customer first name
    cst_lastname NVARCHAR(50),        -- Customer last name
    cst_material_status NVARCHAR(50), -- Customer marital status
    cst_gndr NVARCHAR(50),            -- Customer gender
    cst_create_date DATE              -- Record creation date
);

-- Drop and recreate product information table from CRM source
IF OBJECT_ID('bronze.crm_prd_info', 'U') IS NOT NULL
	DROP TABLE bronze.crm_prd_info;
CREATE TABLE bronze.crm_prd_info (
    prd_id INT,                       -- Unique product identifier
    prd_key NVARCHAR(50),             -- Business product key
    prd_nm NVARCHAR(50),              -- Product name
    prd_cost INT,                     -- Product cost
    prd_lne NVARCHAR(50),             -- Product line
    prd_start_dt DATE,                -- Product availability start date
    prd_end_dt DATE                   -- Product availability end date
);

-- Drop and recreate sales transaction details table from CRM source
IF OBJECT_ID('bronze.sales_details', 'U') IS NOT NULL
	DROP TABLE bronze.sales_details;
CREATE TABLE bronze.sales_details (
    sls_ord_num NVARCHAR(50),         -- Sales order number
    sls_prd_key NVARCHAR(50),         -- Product key linked to product info
    sls_cust_id INT,                  -- Customer ID linked to customer info
    sls_order_dt INT,                 -- Order date (stored as integer format)
    sls_ship_dt INT,                  -- Shipping date (stored as integer format)
    sls_due_dt INT,                   -- Due date (stored as integer format)
    sls_sales INT,                    -- Total sales amount
    sls_quantity INT,                 -- Quantity sold
    sls_price INT                     -- Unit price
);


-- ============================================================================
-- ERP Tables
-- ============================================================================

-- Drop and recreate location reference table from ERP source
IF OBJECT_ID('bronze.erp_loc_a101', 'U') IS NOT NULL
	DROP TABLE bronze.erp_loc_a101;
CREATE TABLE bronze.erp_loc_a101 (
    cid    NVARCHAR(50),              -- Customer ID linked to customer records
    cntry  NVARCHAR(50)               -- Country location code/name
);

-- Drop and recreate customer demographic details table from ERP source
IF OBJECT_ID('bronze.erp_cust_az12', 'U') IS NOT NULL
	DROP TABLE bronze.erp_cust_az12;
CREATE TABLE bronze.erp_cust_az12 (
    cid    NVARCHAR(50),              -- Customer ID
    bdate  DATE,                      -- Customer birth date
    gen    NVARCHAR(50)               -- Customer gender
);

-- Drop and recreate product category table from ERP source
IF OBJECT_ID('bronze.erp_px_cat_g1v2', 'U') IS NOT NULL
	DROP TABLE bronze.erp_px_cat_g1v2;
CREATE TABLE bronze.erp_px_cat_g1v2 (
    id          NVARCHAR(50),         -- Category identifier / Product key link
    cat         NVARCHAR(50),         -- Main product category
    subcat      NVARCHAR(50),         -- Product sub-category
    maintenance NVARCHAR(50)          -- Maintenance requirements flag/details
);
