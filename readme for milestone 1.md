# BC Student Wellness Management System (BC‑SWMS)

> **Course Project · Belgium Campus ITversity**\
> **Project window:** May 2025 – July 2025\
> **Milestone 1 due:** 14 July 2025

A full‑stack solution that helps Belgium Campus students book and manage wellness services (counselling, health appointments, feedback, etc.).\
The deliverable demonstrates mastery of **Core Java, OOP, Swing GUIs, JSP/Servlets, and relational databases** (JavaDB for rapid prototyping, PostgreSQL in production). The entire codebase lives in a GitHub repository to encourage collaboration and rigorous version control.

---

## ✨ Key Features

| Layer                 | Highlights                                                                                                                                           |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Web (JSP/Servlet)** |  • Responsive login & registration pages  • Session‑based authentication  • Secure password hashing  • Dashboard with personalised greeting & logout |
| **Desktop (Swing)**   |  • Rich UI for counsellor calendars, appointment tracking, and student feedback  • MVC architecture to keep UI/logic/data separate                   |
| **Database**          |  • PostgreSQL schema with strict constraints  • Reusable SQL scripts & migrations  • Optionally seed data for demo sessions                          |
| **Collaboration**     |  • GitHub repo with branches, pull requests, Issues, and Projects board  • CI workflow placeholder for future automated tests/deployments            |

---

## 🗂️ Project Structure (Gradle multi‑module)

```text
bc-swms/
├─ desktop-app/        # Swing GUI (runs on JDK‑21+)
├─ web-app/            # JSP + Servlets (WAR for Tomcat 10)
├─ common/             # Shared domain models & utilities
├─ sql/                # DDL, seed data, migrations (Flyway)
└─ docs/               # Design docs, UML, meeting notes
```

---

## 🚀 Getting Started

### 1 · Prerequisites

| Tool           | Version | Notes                                                    |
| -------------- | ------- | -------------------------------------------------------- |
| **JDK**        | 21 LTS  | Install and set `JAVA_HOME`                              |
| **Gradle**     | 8.x     | Wrapper included (`./gradlew`)                           |
| **PostgreSQL** | 15+     | Create a DB named `bc_swms`                              |
| **Tomcat**     | 10.1.x  | For deploying `web-app.war` (or use IDE‑embedded server) |

### 2 · Clone & Build

```bash
git clone https://github.com/YourOrg/bc-swms.git
cd bc-swms
./gradlew clean build  # produces desktop JAR & web WAR
```

### 3 · Database Setup

1. Start PostgreSQL and open a psql shell:
   ```sql
   CREATE DATABASE bc_swms;
   \c bc_swms;
   ```
2. Run the schema script:
   ```sql
   -- sql/schema.sql
   CREATE TABLE users (
     student_number VARCHAR(20) PRIMARY KEY,
     name           VARCHAR(60) NOT NULL,
     surname        VARCHAR(60) NOT NULL,
     email          VARCHAR(120) UNIQUE NOT NULL,
     phone          VARCHAR(20)  NOT NULL,
     password_hash  VARCHAR(255) NOT NULL
   );
   ```
3. (Optional) Execute `sql/seed-data.sql` to insert sample users.

### 4 · Run the Web App

```bash
cp web-app/build/libs/web-app.war $CATALINA_BASE/webapps/
<tomcat>/bin/startup.sh
```

Navigate to `http://localhost:8080/web-app/`.

### 5 · Run the Desktop App

```bash
java -jar desktop-app/build/libs/desktop-app.jar
```

Configure DB connection properties in `desktop-app/src/main/resources/application.properties`.

---

## 🎯 Milestone 1 — Login & Registration

| Requirement                        | Implementation Pointer                                                |
| ---------------------------------- | --------------------------------------------------------------------- |
| **index.jsp**                      | Landing with links to **login.jsp** / **register.jsp**                |
| **register.jsp + RegisterServlet** | Field validation, duplicate‑check, password hashing (BCrypt)          |
| **login.jsp + LoginServlet**       | Credential verification, `HttpSession`, redirect to **dashboard.jsp** |
| **dashboard.jsp**                  | Dynamic greeting `Welcome, ${user.name}!` & Logout button             |
| **Logout**                         | `GET /logout` servlet that invalidates session & redirects to login   |
| **Security**                       | PreparedStatements, HTTPS (in prod), `HttpOnly` & `Secure` cookies    |

---

## 🏗️ Planned Enhancements

- **Role‑based access** (Admin / Counsellor / Student)
- Appointment‑booking calendar with drag‑and‑drop slots
- RESTful API layer (Spring MVC) for mobile clients
- CI pipeline: unit tests → Sonar → Docker image → GitHub Actions deploy

---

## 🤝 Contributing

1. Fork → feature branch (`feat/login-ui`)
2. Commit with conventional messages
3. Open a Pull Request & request code review
4. After approval, squash‑merge into `main`

See [`docs/CONTRIBUTING.md`](docs/CONTRIBUTING.md) for full guidelines.

---

## 📝 License

This project is licensed under the **MIT License** – see [`LICENSE`](LICENSE) for details.

---

## 👥 Authors & Acknowledgements

- **Project Lead:** *Your Name*
- **Team:** *Member A*, *Member B*, *Member C*
- Special thanks to Belgium Campus lecturers for guidance and code review.

---

> Ready to code? Fork the repo, grab an Issue, and let’s build wellness together! ✌️

