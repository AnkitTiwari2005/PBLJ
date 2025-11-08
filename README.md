# SmartQuizApp 🎯

A modern, feature-rich online quiz application built with **Spring Boot** that allows admins to create quizzes and students to take them with real-time scoring and leaderboards.

---

## ✨ Features

### 🎓 For Students
- **Take Quizzes**: Participate in available quizzes with timed sessions  
- **Real-time Timer**: Countdown timer for each quiz attempt  
- **Instant Results**: Immediate scoring after quiz submission  
- **Leaderboards**: View rankings and compare performance with peers  
- **User Registration**: Simple sign-up process  

### 👨‍💼 For Admins
- **Quiz Management**: Create, edit, and delete quizzes  
- **Question Bank**: Add multiple-choice questions with options  
- **Automatic Scoring**: System automatically evaluates and scores attempts  
- **Analytics**: View quiz statistics and performance metrics  
- **User Management**: Monitor student progress and results  

---

## 🚀 Quick Start

### Prerequisites
- Java 17 or higher  
- Maven 3.6+  
- MySQL 8.0+  

### Installation & Running

Clone the repository

git clone <your-repo-url>
cd SmartQuizApp
Build and run the application

mvn clean package spring-boot:run

text

### Database Setup

CREATE DATABASE smartquizapp;

text

### Configuration
Update `src/main/resources/application.properties`:

spring.datasource.url=jdbc:mysql://localhost:3306/smartquizapp
spring.datasource.username=your_username
spring.datasource.password=your_password

text

### Access the Application
- **URL**: http://localhost:8080  
- **Admin**: `admin` / `admin`  
- **Student**: Register new account or use demo  

---

## 🏗️ Project Structure

src/main/java/com/example/smartquizapp/
├── controller/
│ ├── AdminController.java
│ ├── AuthController.java
│ └── QuizController.java
├── model/
│ ├── User.java
│ ├── Quiz.java
│ ├── Question.java
│ └── Attempt.java
├── repository/
│ ├── UserRepository.java
│ ├── QuizRepository.java
│ ├── QuestionRepository.java
│ └── AttemptRepository.java
├── service/
│ └── QuizService.java
└── SmartQuizAppApplication.java

text

---

## 🛠️ Technology Stack

- **Backend**: Spring Boot 3.2.5, Spring MVC, Spring Data JPA  
- **Frontend**: Thymeleaf, Bootstrap 5, JavaScript  
- **Database**: MySQL 8.0 with Hibernate ORM  
- **Build Tool**: Maven  
- **Java Version**: 17  

---

## 📊 Database Schema

-- User table
CREATE TABLE user (
id BIGINT AUTO_INCREMENT PRIMARY KEY,
username VARCHAR(50) UNIQUE NOT NULL,
password VARCHAR(255) NOT NULL,
role ENUM('ADMIN','STUDENT') NOT NULL DEFAULT 'STUDENT',
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Quiz table
CREATE TABLE quiz (
id BIGINT AUTO_INCREMENT PRIMARY KEY,
title VARCHAR(255) NOT NULL,
duration_seconds INT NOT NULL DEFAULT 300,
created_by BIGINT NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Question table
CREATE TABLE question (
id BIGINT AUTO_INCREMENT PRIMARY KEY,
quiz_id BIGINT NOT NULL,
text TEXT NOT NULL,
option_a TEXT NOT NULL,
option_b TEXT NOT NULL,
option_c TEXT,
option_d TEXT,
correct_option ENUM('A','B','C','D') NOT NULL,
marks INT NOT NULL DEFAULT 5
);

-- Attempt table
CREATE TABLE attempt (
id BIGINT AUTO_INCREMENT PRIMARY KEY,
student_id BIGINT NOT NULL,
quiz_id BIGINT NOT NULL,
score INT NOT NULL DEFAULT 0,
max_score INT NOT NULL DEFAULT 0,
started_at DATETIME NOT NULL,
finished_at DATETIME,
answers_json JSON
);

text

---

## 🔧 API Endpoints

| Method | Endpoint | Description |
|--------|-----------|-------------|
| GET/POST | `/login` | User authentication |
| GET/POST | `/register` | User registration |
| GET | `/logout` | User logout |
| GET | `/quizzes` | List all quizzes |
| GET | `/quizzes/{id}/start` | Start quiz attempt |
| POST | `/quizzes/{id}/submit` | Submit quiz answers |
| GET | `/quizzes/{id}/leaderboard` | View leaderboard |
| GET | `/admin/dashboard` | Admin dashboard |
| GET/POST | `/admin/quiz/new` | Create new quiz |
| GET/POST | `/admin/quiz/{id}/question/new` | Add question to quiz |
| POST | `/admin/quiz/{id}/delete` | Delete quiz |

---

## ⚙️ Configuration

### Application Properties

Server Configuration

server.port=8080
server.servlet.session.timeout=1800
Database Configuration

spring.datasource.url=jdbc:mysql://localhost:3306/smartquizapp
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
Thymeleaf Configuration

spring.thymeleaf.cache=false
spring.thymeleaf.prefix=classpath:/templates/
spring.thymeleaf.suffix=.html
Custom Settings

app.quiz.default-duration=300
app.quiz.max-questions=50
Logging

logging.level.com.example.smartquizapp=DEBUG

text

---

## 🎯 Core Features

### Quiz Management
- Timed quizzes with configurable duration (default: 5 minutes)  
- Multiple choice questions (2–4 options)  
- Automatic scoring with detailed feedback  
- Persistent score tracking with timestamps  

### User Management
- Role-based access for admins and students  
- Secure login and session handling  
- Individual progress tracking  

### Analytics & Leaderboards
- Real-time leaderboard updates  
- Performance metrics (average scores, completion rates)  
- Comparative peer analysis  

---

## 🐛 Troubleshooting

### Common Issues & Solutions

**1. Database Connection Issues**

Verify MySQL service is running

sudo systemctl status mysql
Check database exists

mysql -u root -p -e "SHOW DATABASES;"

text

**2. Build Failures**

Clean and rebuild

mvn clean package
Verify Java version

java -version
Clear Maven cache

mvn dependency:purge-local-repository

text

**3. Application Startup Issues**

Enable debug logging

logging.level.org.springframework=DEBUG
logging.level.org.hibernate=DEBUG
Check port availability

netstat -tulpn | grep 8080

text

**4. Quiz Evaluation Problems**

// Debugging in QuizService
System.out.println("Question ID: " + question.getId());
System.out.println("User Answer: " + userAnswer);
System.out.println("Correct Answer: " + correctAnswer);

text

### Debug Mode

Detailed debug configuration

logging.level.com.example.smartquizapp=TRACE
logging.level.org.hibernate.SQL=DEBUG
logging.level.org.hibernate.type.descriptor.sql.BasicBinder=TRACE
logging.level.org.springframework.web=DEBUG
logging.level.org.thymeleaf=DEBUG

text

---

## 🚀 Deployment

### Local Development

mvn spring-boot:run
Or

mvn clean package
java -jar target/smartquizapp-0.0.1-SNAPSHOT.jar

text

### Production Deployment

Build with tests

mvn clean package
Run with production profile

java -jar -Dspring.profiles.active=prod target/smartquizapp-0.0.1-SNAPSHOT.jar
Run on custom port

java -jar -Dserver.port=8080 target/smartquizapp-0.0.1-SNAPSHOT.jar

text

### Docker Deployment

Dockerfile

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

text
undefined

Build and run with Docker

docker build -t smartquizapp .
docker run -p 8080:8080 smartquizapp

text

Docker Compose:

docker-compose up -d

text

---

## 📈 Future Enhancements

- [ ] Email notifications for quiz results  
- [ ] Question categories and tags  
- [ ] Advanced analytics and reporting  
- [ ] Question image support  
- [ ] Export results to PDF/Excel  
- [ ] REST API for mobile apps  
- [ ] Social features and sharing  
- [ ] Advanced question types  
- [ ] Bulk question import  
- [ ] Time-based quiz availability  
- [ ] Question randomization  
- [ ] Custom scoring rules  

---

## 🤝 Contributing

1. Fork the repository  
2. Create feature branch: `git checkout -b feature/amazing-feature`  
3. Commit changes: `git commit -m 'Add amazing feature'`  
4. Push to branch: `git push origin feature/amazing-feature`  
5. Open Pull Request  

### Development Setup

Clone and setup

git clone https://github.com/yourusername/SmartQuizApp.git
cd SmartQuizApp
Create development branch

git checkout -b development
Install dependencies

mvn clean install

text

---

## 📄 License

This project is licensed under the **MIT License**.  
See [LICENSE](LICENSE) for details.

---

## 👥 Default Accounts

| Role | Username | Password | Access |
|------|-----------|----------|--------|
| Admin | `admin` | `admin` | Full system access |
| Student | `student` | `student` | Quiz participation |

---

## 🔍 Monitoring & Logs

### Application Logs

View application logs

tail -f logs/application.log
Enable Spring Security debug logs

logging.level.org.springframework.security=DEBUG

text

### Database Monitoring

-- Monitor ongoing quiz attempts
SELECT * FROM attempt WHERE finished_at IS NULL;

-- View quiz statistics
SELECT quiz_id, COUNT(*) AS attempts, AVG(score) AS avg_score
FROM attempt
GROUP BY quiz_id;

text

### Performance Monitoring

Enable Actuator endpoints

management.endpoints.web.exposure.include=health,metrics,info
management.endpoint.health.show-details=always

text

---

**Built with ❤️ using Spring Boot & Modern Web Technologies**

*For support, check the troubleshooting section or create an issue in the repository.*
