# 🎯 SmartQuizApp — Modern Online Quiz Platform

A **feature-rich**, **responsive**, and **intelligent** quiz application built with **Spring Boot**, empowering admins to manage quizzes and students to compete with **real-time scoring**, **leaderboards**, and **analytics**.

---

## 🚀 Table of Contents

- [✨ Features](#-features)
- [🧰 Prerequisites](#-prerequisites)
- [⚙️ Installation & Setup](#️-installation--setup)
- [🧩 Project Structure](#-project-structure)
- [🛠️ Technology Stack](#️-technology-stack)
- [🗄️ Database Schema](#️-database-schema)
- [📡 API Endpoints](#-api-endpoints)
- [📊 Core Functionalities](#-core-functionalities)
- [🐛 Troubleshooting](#-troubleshooting)
- [🚀 Deployment](#-deployment)
- [📈 Future Enhancements](#-future-enhancements)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)
- [👥 Default Accounts](#-default-accounts)

---

## ✨ Features

### 🎓 For Students
- 🧠 Participate in timed quizzes with **real-time countdown**  
- ⚡ **Instant results** and performance insights  
- 🏆 **Leaderboards** with rank comparison  
- 🔐 Simple and secure **registration/login**  

### 👨‍💼 For Admins
- 🧩 Create, edit, and manage quizzes effortlessly  
- 🗃️ Maintain a **question bank** with multiple options  
- ⚙️ **Auto-evaluation** and score calculation  
- 📈 Monitor performance analytics & user progress  

---

## 🧰 Prerequisites

Ensure you have the following installed:

- ☕ **Java 17+**
- 🧱 **Maven 3.6+**
- 🐬 **MySQL 8.0+**

---

## ⚙️ Installation & Setup

### 1️⃣ Clone Repository
```bash
git clone https://github.com/yourusername/SmartQuizApp.git
cd SmartQuizApp
```

### 2️⃣ Database Setup
```sql
CREATE DATABASE smartquizapp;
```

### 3️⃣ Configure Application Properties
Edit `src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/smartquizapp
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
server.port=8080
```

### 4️⃣ Run Application
```bash
mvn clean package spring-boot:run
```
or
```bash
java -jar target/smartquizapp-0.0.1-SNAPSHOT.jar
```

### 5️⃣ Access Application
🌐 URL → [http://localhost:8080](http://localhost:8080)

---

## 🧩 Project Structure

```
src/main/java/com/example/smartquizapp/
├── controller/
│   ├── AdminController.java
│   ├── AuthController.java
│   └── QuizController.java
├── model/
│   ├── User.java
│   ├── Quiz.java
│   ├── Question.java
│   └── Attempt.java
├── repository/
│   ├── UserRepository.java
│   ├── QuizRepository.java
│   ├── QuestionRepository.java
│   └── AttemptRepository.java
├── service/
│   └── QuizService.java
└── SmartQuizAppApplication.java
```

---

## 🛠️ Technology Stack

| Layer | Technology |
|--------|-------------|
| Backend | Spring Boot 3.2.5, Spring MVC, Spring Data JPA |
| Frontend | Thymeleaf, Bootstrap 5, JavaScript |
| Database | MySQL 8.0 (via Hibernate ORM) |
| Build Tool | Maven |
| Java Version | 17 |

---

## 🗄️ Database Schema

### 🧑‍💻 User Table
```sql
CREATE TABLE user (
 id BIGINT AUTO_INCREMENT PRIMARY KEY,
 username VARCHAR(50) UNIQUE NOT NULL,
 password VARCHAR(255) NOT NULL,
 role ENUM('ADMIN','STUDENT') DEFAULT 'STUDENT',
 created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 📝 Quiz Table
```sql
CREATE TABLE quiz (
 id BIGINT AUTO_INCREMENT PRIMARY KEY,
 title VARCHAR(255) NOT NULL,
 duration_seconds INT DEFAULT 300,
 created_by BIGINT NOT NULL,
 created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### ❓ Question Table
```sql
CREATE TABLE question (
 id BIGINT AUTO_INCREMENT PRIMARY KEY,
 quiz_id BIGINT NOT NULL,
 text TEXT NOT NULL,
 option_a TEXT NOT NULL,
 option_b TEXT NOT NULL,
 option_c TEXT,
 option_d TEXT,
 correct_option ENUM('A','B','C','D') NOT NULL,
 marks INT DEFAULT 5
);
```

### 🧾 Attempt Table
```sql
CREATE TABLE attempt (
 id BIGINT AUTO_INCREMENT PRIMARY KEY,
 student_id BIGINT NOT NULL,
 quiz_id BIGINT NOT NULL,
 score INT DEFAULT 0,
 max_score INT DEFAULT 0,
 started_at DATETIME NOT NULL,
 finished_at DATETIME,
 answers_json JSON
);
```

---

## 📡 API Endpoints

| Method | Endpoint | Description |
|--------|-----------|-------------|
| GET/POST | `/login` | User authentication |
| GET/POST | `/register` | New user registration |
| GET | `/logout` | Logout user |
| GET | `/quizzes` | View available quizzes |
| GET | `/quizzes/{id}/start` | Start a quiz |
| POST | `/quizzes/{id}/submit` | Submit quiz answers |
| GET | `/quizzes/{id}/leaderboard` | View quiz leaderboard |
| GET | `/admin/dashboard` | Admin dashboard |
| GET/POST | `/admin/quiz/new` | Create new quiz |
| GET/POST | `/admin/quiz/{id}/question/new` | Add questions |
| POST | `/admin/quiz/{id}/delete` | Delete quiz |

---

## 📊 Core Functionalities

### 🧠 Quiz Management
- Configurable duration and question count  
- Auto-grading based on correct answers  
- Persistent scoring with timestamps  

### 👤 User Management
- Role-based access (Admin/Student)  
- Secure authentication and sessions  
- Progress tracking dashboard  

### 📈 Analytics & Leaderboards
- Live leaderboard updates  
- Average scores and participation rate  
- Historical performance tracking  

---

## 🐛 Troubleshooting

| Issue | Solution |
|--------|-----------|
| ❌ MySQL Connection Error | Check MySQL service and credentials |
| 🧱 Build Failure | `mvn clean package` and verify Java version |
| ⚙️ Startup Issue | Enable debug logging and check port `8080` |

Enable Debug Logs:
```properties
logging.level.com.example.smartquizapp=DEBUG
logging.level.org.hibernate.SQL=DEBUG
logging.level.org.springframework.web=DEBUG
```

---

## 🚀 Deployment

### 🖥️ Local
```bash
mvn spring-boot:run
```

### 🧳 Production
```bash
java -jar -Dspring.profiles.active=prod target/smartquizapp-0.0.1-SNAPSHOT.jar
```

### 🐳 Docker
```Dockerfile
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn -DskipTests package

FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /app/target/smartquizapp-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/app.jar"]
```
```bash
docker build -t smartquizapp .
docker run -p 8080:8080 smartquizapp
```

---

## 📈 Future Enhancements

- [ ] Email notifications  
- [ ] Question tagging & categories  
- [ ] Image-based questions  
- [ ] Mobile REST API integration  
- [ ] Advanced analytics dashboard  
- [ ] Randomized question order  
- [ ] PDF/Excel export for results  

---

## 🤝 Contributing

1. **Fork** the repo  
2. Create a **feature branch** (`git checkout -b feature/amazing-feature`)  
3. **Commit** changes (`git commit -m "Add feature"`)  
4. **Push** to branch (`git push origin feature/amazing-feature`)  
5. Open a **Pull Request** 🎉

---

## 📄 License

Licensed under the **MIT License**.  
See [LICENSE](LICENSE) for details.

---

## 👥 Default Accounts

| Role | Username | Password | Access |
|------|-----------|----------|--------|
| Admin | `admin` | `admin` | Full Access |
| Student | `student` | `student` | Quiz Participation |

---

> **Built with ❤️ using Spring Boot, Thymeleaf, and MySQL**  
> *Empowering learning through interactive quizzing.*
