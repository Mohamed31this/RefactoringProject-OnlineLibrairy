# Online Library — raw application baseline

Java web application for library management: registration/login, book search,
book details, borrowing/returns/history, and administrator management pages.

## Origin

Adapted from https://github.com/aymenbbrk/onlinebiblio
Original baseline commit: `c394840efee18e83d911f252f9feeff3dfe66867` (first repository commit).
The application Java sources, JSP/CSS files and database scripts are preserved
byte-for-byte from that commit. This is a prepared baseline, not an unmodified
historical snapshot. Credit for the original application remains with its authors.

## Baseline preparation

- Excluded the original tests and removed JUnit, Mockito, TestNG and explicit
  test-runner configuration from pom.xml.
- Excluded the unrelated package.json, which lists a separate frontend stack.
- Set Maven Java source/target/release to 17 for this baseline.
- Kept Maven dependencies and WAR packaging needed to build the application.
- No Jenkins pipeline, Docker, Kubernetes, SonarQube, coverage tooling,
  Prometheus/Grafana, generated build files or Git history are included.
- Kept application structure, input checks, authentication and authorization.
  These are application behavior and should not be deliberately broken.

## Manual setup

Requirements: JDK 17, Maven, MySQL 8 and Tomcat 10.1.

1. Create and seed the database:

   ```sh
   mysql -u root -p < database/schema.sql
   mysql -u root -p < database/seed.sql
   ```

2. Edit URL, USERNAME and PASSWORD in
   `src/main/java/com/library/util/DatabaseConnection.java` for your local MySQL.
   This class uses its own constants; the db.* context parameters in web.xml
   are not used by that connection class.
3. Build manually:

   ```sh
   mvn clean package
   ```

4. Copy `target/online-library.war` into Tomcat's `webapps/` directory and start
   Tomcat. With the default Tomcat port, open:
   http://localhost:8080/online-library/

The seed script provides admin/admin123 and john_doe/user123 as demo accounts.
This baseline is for local coursework and retains the original implementation's
limitations. Improvements and automated tests can be added as coursework.

## Verification

See VALIDATION.txt for checks performed when preparing this archive.
