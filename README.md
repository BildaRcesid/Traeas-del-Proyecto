# Traeas-del-Proyecto

CREATE DATABASE  IF NOT EXISTS `bd_empresa_producto_limpieza` /*!40100 DEFAULT CHARACTER SET utf8 */ /*!80016 DEFAULT ENCRYPTION='N' */;


USE `bd_empresa_producto_limpieza`;
-- MySQL dump 10.13  Distrib 8.0.19, for Win64 (x86_64)
--
-- Host: 127.0.0.1    Database: bd_empresa_producto_limpieza

Table structure for table `cargo_laboral`

--
DROP TABLE IF EXISTS `cargo_laboral`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `cargo_laboral` (
  `id_` int NOT NULL,
  `cargo_laboral` varchar(45) NOT NULL,
  `descripcion` text NOT NULL,
  `salario_mensual` float NOT NULL,
  PRIMARY KEY (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `cargo_laboral`
--

LOCK TABLES `cargo_laboral` WRITE;
/*!40000 ALTER TABLE `cargo_laboral` DISABLE KEYS */;
/*!40000 ALTER TABLE `cargo_laboral` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `cliente`
--

DROP TABLE IF EXISTS `cliente`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `cliente` (
  `id_` int NOT NULL,
  `nombres` varchar(60) NOT NULL,
  `apellidos` varchar(60) NOT NULL,
  `nro_identificacion` varchar(12) NOT NULL,
  `sexo` char(1) NOT NULL,
  `celular` varchar(15) NOT NULL,
  `email_personal` varchar(50) NOT NULL,
  `direccion` varchar(45) NOT NULL,
  `fecha` date NOT NULL,
  `pedidos_id` int NOT NULL,
  `factura_id` int NOT NULL,
  `forma_pago_id` int NOT NULL,
  PRIMARY KEY (`id_`),
  KEY `fk_cliente_pedidos_idx` (`pedidos_id`),
  KEY `fk_cliente_factura_idx` (`factura_id`),
  KEY `fk_cliente_forma_pago_idx` (`forma_pago_id`),
  CONSTRAINT `fk_cliente_factura` FOREIGN KEY (`factura_id`) REFERENCES `factura` (`id_`),
  CONSTRAINT `fk_cliente_forma_pago` FOREIGN KEY (`forma_pago_id`) REFERENCES `forma_pago` (`id_`),
  CONSTRAINT `fk_cliente_pedidos` FOREIGN KEY (`pedidos_id`) REFERENCES `pedidos` (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `cliente`
--

LOCK TABLES `cliente` WRITE;
/*!40000 ALTER TABLE `cliente` DISABLE KEYS */;
/*!40000 ALTER TABLE `cliente` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `det_factura`
--

DROP TABLE IF EXISTS `det_factura`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `det_factura` (
  `factura_id` int NOT NULL,
  `producto_id` int NOT NULL,
  KEY `fk_det_factura_factura_idx` (`factura_id`),
  KEY `fk_det_factura_productos_idx` (`producto_id`),
  CONSTRAINT `fk_det_factura_factura` FOREIGN KEY (`factura_id`) REFERENCES `factura` (`id_`),
  CONSTRAINT `fk_det_factura_productos` FOREIGN KEY (`producto_id`) REFERENCES `productos` (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `det_factura`
--

LOCK TABLES `det_factura` WRITE;
/*!40000 ALTER TABLE `det_factura` DISABLE KEYS */;
/*!40000 ALTER TABLE `det_factura` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `empleado`
--

DROP TABLE IF EXISTS `empleado`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `empleado` (
  `id_` int NOT NULL,
  `nombre` varchar(50) NOT NULL,
  `apellidos` varchar(50) NOT NULL,
  `nro_identificacion` varchar(65) NOT NULL,
  `sexo` char(1) NOT NULL,
  `celular` varchar(45) NOT NULL,
  `email_personal` varchar(70) NOT NULL,
  `direccion` varchar(45) NOT NULL,
  `fecha_ingreso` date NOT NULL,
  `factura_id` int NOT NULL,
  `cargo_laboral` int NOT NULL,
  PRIMARY KEY (`id_`),
  UNIQUE KEY `id__UNIQUE` (`id_`),
  KEY `fk_empleado_factura_idx` (`factura_id`),
  KEY `fk_empleado_cargo_laboral_idx` (`cargo_laboral`),
  CONSTRAINT `fk_empleado_cargo_laboral` FOREIGN KEY (`cargo_laboral`) REFERENCES `cargo_laboral` (`id_`),
  CONSTRAINT `fk_empleado_factura` FOREIGN KEY (`factura_id`) REFERENCES `factura` (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `empleado`
--

LOCK TABLES `empleado` WRITE;
/*!40000 ALTER TABLE `empleado` DISABLE KEYS */;
/*!40000 ALTER TABLE `empleado` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `factura`
--

DROP TABLE IF EXISTS `factura`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `factura` (
  `id_` int NOT NULL,
  `fecha` date NOT NULL,
  `codigo` varchar(15) NOT NULL,
  `descripcion` varchar(100) NOT NULL,
  `total` double NOT NULL,
  PRIMARY KEY (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `factura`
--

LOCK TABLES `factura` WRITE;
/*!40000 ALTER TABLE `factura` DISABLE KEYS */;
/*!40000 ALTER TABLE `factura` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `factura_compra`
--

DROP TABLE IF EXISTS `factura_compra`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `factura_compra` (
  `id_` int NOT NULL,
  `fecha` date NOT NULL,
  `codigo` varchar(45) NOT NULL,
  `descripcion` varchar(200) NOT NULL,
  `total` double NOT NULL,
  PRIMARY KEY (`id_`),
  UNIQUE KEY `fecha_UNIQUE` (`fecha`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `factura_compra`
--

LOCK TABLES `factura_compra` WRITE;
/*!40000 ALTER TABLE `factura_compra` DISABLE KEYS */;
/*!40000 ALTER TABLE `factura_compra` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `forma_pago`
--

DROP TABLE IF EXISTS `forma_pago`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `forma_pago` (
  `id_` int NOT NULL,
  `tarjeta` int NOT NULL,
  `efectivo` int NOT NULL,
  `factura_id` int NOT NULL,
  PRIMARY KEY (`id_`),
  KEY `fk_forma_pago_factura_idx` (`factura_id`),
  CONSTRAINT `fk_forma_pago_factura` FOREIGN KEY (`factura_id`) REFERENCES `factura` (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `forma_pago`
--

LOCK TABLES `forma_pago` WRITE;
/*!40000 ALTER TABLE `forma_pago` DISABLE KEYS */;
/*!40000 ALTER TABLE `forma_pago` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `jornada_laboral`
--

DROP TABLE IF EXISTS `jornada_laboral`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `jornada_laboral` (
  `id_` int NOT NULL,
  `hora_entrada` datetime NOT NULL,
  `hora_salida` datetime NOT NULL,
  `empleado_id` int NOT NULL,
  PRIMARY KEY (`id_`),
  KEY `fk_jornada_laboral_empleado_idx` (`empleado_id`),
  CONSTRAINT `fk_jornada_laboral_empleado` FOREIGN KEY (`empleado_id`) REFERENCES `empleado` (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `jornada_laboral`
--

LOCK TABLES `jornada_laboral` WRITE;
/*!40000 ALTER TABLE `jornada_laboral` DISABLE KEYS */;
/*!40000 ALTER TABLE `jornada_laboral` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `marca_productos`
--

DROP TABLE IF EXISTS `marca_productos`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `marca_productos` (
  `id_` int NOT NULL,
  `descripcion` text NOT NULL,
  `productos_id` int NOT NULL,
  PRIMARY KEY (`id_`),
  KEY `fk_marca_productos_productos_idx` (`productos_id`),
  CONSTRAINT `fk_marca_productos_productos` FOREIGN KEY (`productos_id`) REFERENCES `productos` (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `marca_productos`
--

LOCK TABLES `marca_productos` WRITE;
/*!40000 ALTER TABLE `marca_productos` DISABLE KEYS */;
/*!40000 ALTER TABLE `marca_productos` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `pedidos`
--

DROP TABLE IF EXISTS `pedidos`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `pedidos` (
  `id_` int NOT NULL,
  `fecha` date NOT NULL,
  `total` double NOT NULL,
  PRIMARY KEY (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `pedidos`
--

LOCK TABLES `pedidos` WRITE;
/*!40000 ALTER TABLE `pedidos` DISABLE KEYS */;
/*!40000 ALTER TABLE `pedidos` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `productos`
--

DROP TABLE IF EXISTS `productos`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `productos` (
  `id_` int NOT NULL,
  `codigo` varchar(45) NOT NULL,
  `precio` int NOT NULL,
  `descripcion` text NOT NULL,
  `fecha_vencimiento` date NOT NULL,
  `fecha_elaboracion` date NOT NULL,
  `pedidos_id` int NOT NULL,
  `proveedor_id` int NOT NULL,
  `tipo_productos` int NOT NULL,
  PRIMARY KEY (`id_`),
  KEY `fk_productos_pedidos_idx` (`pedidos_id`),
  KEY `fk_productos_proveedor_idx` (`proveedor_id`),
  KEY `fk_productos_tipo_productos_idx` (`tipo_productos`),
  CONSTRAINT `fk_productos_pedidos` FOREIGN KEY (`pedidos_id`) REFERENCES `pedidos` (`id_`),
  CONSTRAINT `fk_productos_proveedor` FOREIGN KEY (`proveedor_id`) REFERENCES `proveedor` (`id`),
  CONSTRAINT `fk_productos_tipo_productos` FOREIGN KEY (`tipo_productos`) REFERENCES `tipo_productos` (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `productos`
--

LOCK TABLES `productos` WRITE;
/*!40000 ALTER TABLE `productos` DISABLE KEYS */;
/*!40000 ALTER TABLE `productos` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `proveedor`
--

DROP TABLE IF EXISTS `proveedor`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `proveedor` (
  `id` int NOT NULL,
  `nombre_proveedor` varchar(65) NOT NULL,
  `factura_compra_id` int NOT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_proveedor_factura_compra_idx` (`factura_compra_id`),
  CONSTRAINT `fk_proveedor_factura_compra` FOREIGN KEY (`factura_compra_id`) REFERENCES `factura_compra` (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `proveedor`
--

LOCK TABLES `proveedor` WRITE;
/*!40000 ALTER TABLE `proveedor` DISABLE KEYS */;
/*!40000 ALTER TABLE `proveedor` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `tipo_productos`
--

DROP TABLE IF EXISTS `tipo_productos`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `tipo_productos` (
  `id_` int NOT NULL,
  `descripcion` text NOT NULL,
  PRIMARY KEY (`id_`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `tipo_productos`
--

LOCK TABLES `tipo_productos` WRITE;
/*!40000 ALTER TABLE `tipo_productos` DISABLE KEYS */;
/*!40000 ALTER TABLE `tipo_productos` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Dumping events for database 'bd_empresa_producto_limpieza'
--
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2021-11-02 12:37:16
