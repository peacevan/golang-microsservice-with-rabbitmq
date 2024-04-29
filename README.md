

---

# E-commerce Microservices with Go-lang and RabbitMQ

## Overview
This repository contains two microservices implemented in Go (Golang), utilizing ORM for data persistence and following the principles of clean architecture. Integrated with RabbitMQ for asynchronous messaging, these microservices facilitate efficient communication within a distributed e-commerce system, focusing on backend functionalities.

## Modules
1. **Microservice E-commerce (microsservice-ecommerce):**
   - Implements order management functionalities using clean architecture principles.
   - Utilizes ORM for data persistence.
   - Leverages parallelism for efficient order processing.
   - Notifies the admin backend about order-related actions via RabbitMQ.

2. **Microservice E-commerce Admin (microsservice-ecommerce-admin):**
   - Processes order notifications and records daily sales.
   - Utilizes ORM for data persistence and clean architecture principles.
   - Implements parallel processing for efficient inventory updates.
   - Notifies the ecommerce backend about inventory updates via RabbitMQ.
   - Periodically synchronizes inventory with the ecommerce backend.

## Getting Started
To get started with this project, follow these steps:

1. **Clone the Repository:** `git clone https://github.com/peacevan/golang-microsservice-with-rabbitmq.git`
2. **Navigate to Submodules:** Enter the directories for `microsservice-ecommerce` and `microsservice-ecommerce-admin`.
3. **Install Dependencies:** Ensure Go, ORM library (e.g., GORM), and RabbitMQ are installed on your system.
4. **Configuration:** Update the configuration files as needed to match your environment.
5. **Build and Run:** Build the microservices using `go build` and run them using `./<executable_name>`.

## Usage
Once the microservices are up and running, the ecommerce backend can be used to manage orders, while the admin backend processes orders, updates sales and inventory, and synchronizes inventory with the ecommerce backend.

## Contributing
Contributions are welcome! If you find any issues or have suggestions for improvements, please feel free to open an issue or create a pull request.

## License
This project is licensed under the [MIT License](LICENSE).

---

Feel free to customize and expand upon this template to better suit the specifics of your project!
