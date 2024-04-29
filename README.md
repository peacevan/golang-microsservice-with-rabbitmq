Aqui está uma versão revisada do README, levando em consideração os requisitos e os submódulos mencionados:

---

# E-commerce Microservices with RabbitMQ

## Overview
This repository contains two microservices implemented in Go (Golang) and integrated with RabbitMQ for asynchronous messaging. The microservices are designed to facilitate efficient communication within a distributed e-commerce system, specifically focusing on the frontend (microsservice-ecommerce) and the backend (microsservice-ecommerce-admin) functionalities.

## Modules
1. **Frontend (microsservice-ecommerce):**
   - Registers, cancels, and completes orders.
   - Notifies the backend about order-related actions.

2. **Backend (microsservice-ecommerce-admin):**
   - Reads order notifications and records daily sales.
   - Updates sales and inventory upon order completion.
   - Notifies the frontend about inventory updates.
   - Periodically synchronizes inventory with the frontend.

## Getting Started
To get started with this project, follow these steps:

1. **Clone the Repository:** `git clone https://github.com/peacevan/golang-microsservice-with-rabbitmq.git`
2. **Navigate to Submodules:** Enter the directories for `microsservice-ecommerce` and `microsservice-ecommerce-admin`.
3. **Install Dependencies:** Ensure Go and RabbitMQ are installed on your system.
4. **Configuration:** Update the configuration files as needed to match your environment.
5. **Build and Run:** Build the microservices using `go build` and run them using `./<executable_name>`.

## Usage
Once the microservices are up and running, the frontend can be used to register, cancel, and complete orders. The backend will process these orders, update sales and inventory accordingly, and synchronize inventory with the frontend.

## Contributing
Contributions are welcome! If you find any issues or have suggestions for improvements, please feel free to open an issue or create a pull request.

## License
This project is licensed under the [MIT License](LICENSE).

---

Feel free to customize and expand upon this template to better suit the specifics of your project!
