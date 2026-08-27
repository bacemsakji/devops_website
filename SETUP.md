# Setup Instructions for E-Commerce Website

## Prerequisites

1. **Java Development Kit (JDK)** - JDK 8 or higher
2. **Apache Maven** - For building the project
3. **Apache Tomcat** - Version 9.x or higher (servlet container)
4. **MySQL Server** - Version 5.7 or higher

## Database Setup

1. **Install MySQL Server** if not already installed
2. **Start MySQL Service**
3. **Create Database**:
   ```sql
   CREATE DATABASE mycart;
   ```
4. **Update Database Credentials** (if needed):
   - Edit `src/main/resources/hibernate.cfg.xml`
   - Update the following properties:
     ```xml
     <property name="connection.username">root</property>
     <property name="connection.password">your_password</property>
     ```
   - Default username is `root` with empty password

## Building the Project

1. Open a terminal/command prompt in the project directory
2. Run the Maven build command:
   ```bash
   mvn clean package
   ```
3. This will create a WAR file at: `target/mycart.war`

## Deploying to Tomcat

### Option 1: Manual Deployment
1. Copy `target/mycart.war` to your Tomcat `webapps` directory
   - Example: `C:\Program Files\Apache Software Foundation\Tomcat 9.0\webapps\`
2. Start Tomcat server
3. Access the application at: `http://localhost:8080/mycart`

### Option 2: Using Maven Tomcat Plugin
1. Add the following to your `pom.xml` in the `<plugins>` section:
   ```xml
   <plugin>
     <groupId>org.apache.tomcat.maven</groupId>
     <artifactId>tomcat7-maven-plugin</artifactId>
     <version>2.2</version>
     <configuration>
       <path>/mycart</path>
       <port>8080</port>
     </configuration>
   </plugin>
   ```
2. Run: `mvn tomcat7:deploy`
3. Access at: `http://localhost:8080/mycart`

## Running the Application

1. Ensure MySQL is running
2. Start Tomcat server
3. Open browser and navigate to: `http://localhost:8080/mycart`
4. The application will automatically create required tables on first run (due to `hbm2ddl.auto=update`)

## Application Features

### Admin Access
- Add New Products
- Add New Category
- View Available Products
- View Current Users
- View Category
- Remove Products

### User Access
- Create New Account or Register
- Login
- View Available Products
- Select Product to Buy
- Select Product Quantity
- Add To cart
- Go to Checkout Page

## Troubleshooting

### Database Connection Issues
- Verify MySQL is running
- Check credentials in `hibernate.cfg.xml`
- Ensure the database `mycart` exists

### Port Already in Use
- Change Tomcat port in `server.xml` or use a different port
- Default Tomcat port is 8080

### Build Errors
- Ensure Maven is properly installed: `mvn -version`
- Clean and rebuild: `mvn clean install`
