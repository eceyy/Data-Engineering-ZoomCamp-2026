# Data Engineering Zoomcamp 2026
## Module 1 Homework – Docker & SQL & Terraform

This repository contains my solutions for Module 1 Homework of the DataTalksClub Data Engineering Zoomcamp.

---

## Question 1: Understanding Docker Images

**Question:**  
Run docker with the `python:3.13` image. What is the version of pip?

**Command used:**
```bash
docker run -it --entrypoint bash python:3.13
pip --version
