# Assignment 6 — Deploy the Book Review App with Docker Compose

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will deploy the Book Review Application with Docker Compose using MySQL, a backend API, and a frontend user interface. You will configure health-gated startup, browser-facing API access, CORS, and persistent MySQL storage.

---

# Task 1 — Prepare the Project

## Goal

Prepare your fork of the Book Review App repository for Docker Compose deployment.

### Evidence

#### Screenshot 1 — Project Structure

Add a screenshot showing the project structure containing:

```text
frontend/
backend/
.env.example
.gitignore
docker-compose.yml
```

![Project Structure](./screenshots/Project-structureASS06.png)

---

#### Screenshot 2 — Environment and Docker Ignore Files

Add a screenshot showing the contents of:

```text
.env.example
.gitignore
frontend/.dockerignore
backend/.dockerignore
```

Ensure that no real passwords, tokens, or secrets are visible.

![Environment and Docker Ignore Files](./screenshots/file-contents.png)

---

# Task 2 — Create or Confirm Application Dockerfiles

## Goal

Prepare Dockerfiles for the frontend and backend services and build both services through Docker Compose.

### Evidence

#### Screenshot 3 — Frontend Dockerfile

Add a screenshot showing the completed `frontend/Dockerfile`.

![Frontend Dockerfile](./screenshots/DF-frontendAS06.png)

---

#### Screenshot 4 — Backend Dockerfile

Add a screenshot showing the completed `backend/Dockerfile`.

![Backend Dockerfile](./screenshots/DF-backendAS06.png).

---

#### Screenshot 5 — Docker Compose Build

Add a screenshot of the terminal showing successful completion of:

```bash
docker compose build
```

![Docker Compose Build](./screenshots/DCB-ASS06.png)

---

# Task 3 — Create the Docker Compose Stack

## Goal

Create one `docker-compose.yml` file that builds and runs MySQL, backend, and frontend services.

### Evidence

#### Screenshot 6 — MySQL Service, Health Check, and Volume Mount

Add a screenshot showing the MySQL service in `docker-compose.yml`, including:

- MySQL image
- Environment variables
- MySQL health check
- `mysql_data` volume mount
- No published MySQL port

![MySQL Service, Health Check, and Volume Mount](./screenshots/DC-updateASS06.png)

---

#### Screenshot 7 — Backend Configuration

Add a screenshot showing the backend service configuration, including:

- `depends_on` with `condition: service_healthy`
- Database host set to `mysql`
- Browser frontend origin configured for CORS
- Published backend port

![Backend Configuration](./screenshots/Backend-ConfigurationASS06.png)

---

#### Screenshot 8 — Frontend Configuration

Add a screenshot showing the frontend service configuration, including:

- Published frontend port
- `depends_on` for the backend service
- Browser-facing `NEXT_PUBLIC_API_URL`

![Frontend Configuration](./screenshots/Frontend-ConfigurationASS06.png)

---

#### Screenshot 9 — Named Volume Definition

Add a screenshot showing the `mysql_data` volume definition in `docker-compose.yml`.

![Named Volume Definition](./screenshots/Named-Volume-DefinitionASS06.png)

---

# Task 4 — Start and Verify the Stack

## Goal

Build and start all services through one Docker Compose workflow.

### Evidence

#### Screenshot 10 — Docker Compose Service Status

Add a screenshot of the terminal showing:

```bash
docker compose ps
```

The output must show the MySQL, backend, and frontend services running. MySQL must show as healthy.

![Docker Compose Service Status](./screenshots/DCPS-ASS06.png)

---

#### Screenshot 11 — MySQL and Backend Logs

Add a screenshot of the terminal showing:

```bash
docker compose logs mysql backend --tail=50
```

The logs must show MySQL readiness and successful backend database connection.

![MySQL and Backend Logs](./screenshots/logs--tail-50ASS06.png)

---

# Task 5 — Test End-to-End Application Functionality

## Goal

Verify that the Book Review App works through the browser.

### Evidence

#### Screenshot 12 — Successful Registration or Login

Add a browser screenshot showing successful user registration or login.

Add your full name as a clear caption directly below the screenshot.

![Successful Registration or Login](./screenshots/loginASS06.png)

---

#### Screenshot 13 — Created Book Review

Add a browser screenshot showing a created book review visible in the application.

Add your full name as a clear caption directly below the screenshot.

![Created Book Review](./screenshots/Created-Book-ReviewASS06.png)

---

#### Screenshot 14 — CORS Verification

Add a browser developer-tools screenshot with:

- The Network tab showing a successful API request
- The Console drawer showing no CORS error after the API interaction

![CORS Verification](./screenshots/CORS-VerificationASS06.png)

---

# Task 6 — Prove MySQL Data Persistence

## Goal

Verify that MySQL data remains after a non-destructive Docker Compose down/up cycle.

### Evidence

#### Screenshot 15 — Data Before Restart

Add a browser screenshot showing the registered user or created review before the down/up cycle.

Add your full name as a clear caption directly below the screenshot.

![Data Before Restart](./screenshots/Created-Book-ReviewASS06.png)

---

#### Screenshot 16 — Non-Destructive Stack Restart

Add a screenshot of the terminal showing the non-destructive shutdown and restart:

```bash
docker compose down
docker compose up -d
docker compose ps
```

Do not use `docker compose down -v`.

![Non-Destructive Stack Restart](./screenshots/CMD-ASS06.png)

---

#### Screenshot 17 — Data After Restart

Add a browser screenshot showing the same registered user or review after the stack restarts.

Add your full name as a clear caption directly below the screenshot.

![Data After Restart](./screenshots/Consistent-ASSO6.png)

---

# Task 7 — Explain Docker Compose Teardown Modes

## Goal

Explain the difference between preserving data and fully resetting a Docker Compose environment.

### Notes

Write a short explanation of 5–8 lines covering:

- What `docker compose down` removes and preserves
- Why named volumes should be kept when preserving MySQL data
- What happens when named volumes are removed
- When a full reset is useful
- Why a full reset must not be used before persistence evidence is captured

docker compose down stops and removes containers and the Compose-created network, but preserves named volumes such as mysql_data, so MySQL data survives a teardown. Because the volume is named (not anonymous), it is reattached on the next up, which is why named volumes must be kept when preserving database state. Adding the -v flag (docker compose down -v) deletes named volumes, so the next startup re-initializes MySQL from scratch and all stored rows are lost. A full reset is useful when schema, credentials, or .env values change and stale data blocks progress. It must never be used before persistence evidence is captured, because once the volume is removed the data cannot be recovered. In summary: plain down preserves state; down -v destroys it and should be used deliberately.

---

# Final Public Frontend URL

**Frontend URL:** `http://3.91.43.42:3000/book/1`

Replace the placeholder with your working application URL.

---

# GitHub Repository URL

**Your Fork or Repository URL:** `https://github.com/Judahforge/book-review-app`

---

# LinkedIn Requirement

## Goal

Create a LinkedIn post about the Book Review App deployment and what you learned from using Docker Compose.

### Evidence

**LinkedIn Post URL:** `https://lnkd.in/p/dhWe9xmD`

#### LinkedIn Post Screenshot

![LinkedIn Post Screenshot](./screenshots/Linkedin-Ass06.png)

---

# Submission Checklist

- [ ] Book Review App repository forked and used
- [ ] `.env` excluded from Git tracking
- [ ] `.env.example` contains only safe placeholder values
- [ ] Frontend and backend Dockerfiles created or confirmed
- [ ] MySQL health check configured
- [ ] Backend waits for healthy MySQL
- [ ] Backend uses `mysql` as the database hostname
- [ ] Frontend API URL uses the VM public IP and backend port
- [ ] Backend CORS origin matches the frontend origin
- [ ] MySQL port 3306 is not publicly exposed
- [ ] Registration and login work
- [ ] Book review creation works
- [ ] Data persists after a non-destructive down/up cycle
- [ ] Screenshots 1–17 included
- [ ] Teardown explanation completed
- [ ] Public frontend URL included
- [ ] GitHub repository URL included
- [ ] LinkedIn post URL and screenshot included
- [ ] Full name visible in required terminal screenshots
- [ ] Browser screenshots include a full-name caption
- [ ] No sensitive information exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*
