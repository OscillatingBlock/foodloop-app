
# FoodLoop Backend

This repository contains the backend for **FoodLoop**, an application designed to combat food waste by creating a direct link between food retailers, farmers, and Non-Profit Organizations (NGOs). The platform aims to facilitate the efficient distribution of surplus food to those in need, reducing waste and supporting communities.

This project was proudly developed during my **first hackathon**. It served as an invaluable learning experience in rapid development, API design, database integration, and working collaboratively under time constraints.


![image](https://github.com/user-attachments/assets/873bbfe5-05de-4a6a-823e-047a48d2e2eb)


## Features

* **User Authentication & Authorization:** Secure sign-up, login, and role-based access control (Retailer, Farmer, NGO) using JWT.
* **Retailer & Farmer Inventory:** Functionality for users to manage their food stock, including adding new items, updating quantities, and marking items for donation.
* **NGO Demand & Requests:** NGOs can view available food listings based on their location and place requests for needed items.
* **Request Management Workflow:** Retailers and Farmers can view, approve, or ignore incoming requests from NGOs.
* **Farmer Demand Forecasting:** Provides farmers with basic market analysis and demand forecasts based on regional historical NGO request data, offering insights into what items are frequently needed.
* **AI-Powered Date Estimation:** Utilizes the Google Gemini API to provide more realistic 'best before' and 'expires at' date estimations for new food items, considering factors like location and season.
* **Database Integration:** Structured data storage and management using SQLAlchemy.
* **Notifications:** Basic notification system to alert retailers/farmers about new requests or expiring items.

## Technologies Used

* **Flask:** A lightweight Python web framework.
* **SQLAlchemy:** Python SQL Toolkit and Object Relational Mapper.
* **Flask-JWT-Extended:** For adding JWT support to Flask endpoints.
* **Flask-Security-Too:** Provides security features like role management.
* **python-dotenv:** For managing environment variables.
* **Google Generative AI (Gemini API):** Integrated for intelligent date estimation and demand analysis.

## Getting Started

Follow these steps to set up and run the FoodLoop backend locally:

### Prerequisites

* Python 3.6+
* pip (Python package installer)
* A database system (e.g., PostgreSQL, SQLite, MySQL). The current configuration uses `[Specify your database]`.

### 1. Clone the Repository

```bash
git clone [https://github.com/OscillatingBlock/foodloop-app/]
cd foodloop-app
```

### 2. Create and Activate a Virtual Environment

It's recommended to use a virtual environment to manage dependencies.

```bash
# For venv
python -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`

# Or for virtualenv
virtualenv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
```

### 3. Install Dependencies

Install the required Python packages.

```bash
pip install -r requirements.txt
```

### 4. Environment Configuration

Create a `.env` file in the root directory of the repository. This file will store sensitive information and configuration variables.

```ini
# .env
SECRET_KEY='[A strong, random secret key for Flask sessions]'
SECURITY_PASSWORD_SALT='[A strong, random salt for password hashing]'

# Google Gemini API Configuration
GEMINI_API_KEY='[Your Google Gemini API Key]'

```


### 5. Database Setup

Since not using flask migrate for now , just runnning the run.py will initialise the db.

### 6. Running the Application

Start the Flask development server.

```bash
python run.py
```

The backend should now be running locally, typically at `http://127.0.0.1:5000`.

## API Endpoints

The backend exposes various API endpoints for different functionalities. Refer to the API documentation for details on available routes, methods, and request/response formats.


### API Documentation

| Method   | Endpoint                       | Description                                                                  | Authentication    |
| :------- | :----------------------------- | :--------------------------------------------------------------------------- | :---------------- |
| `POST`   | `/sign-up`                     | Create a new user account                                                    | None              |
| `POST`   | `/login`                       | Authenticate user                                                            | None              |
| `POST`   | `/logout`                      | Log out the current user                                                     | None              |
| `GET`    | `/ngo/filtered_food`           | Get listed food items filtered by pincode                                    | NGO Required      |
| `POST`   | `/ngo/request/<int:id>`        | NGO requests a specific listed food item                                     | NGO Required      |
| `GET`    | `/ngo/my_requests`             | Get requests made by the authenticated NGO                                   | NGO Required      |
| `POST`   | `/ngo/claim/<int:id>`          | NGO claims a specific approved food item                                     | NGO Required      |
| `GET`    | `/retailers/inventory`         | Get authenticated retailer's food inventory                                  | Retailer Req.     |
| `POST`   | `/retailers/add_item`          | Add a new food item (batch) to inventory                                     | Retailer Req.     |
| `DELETE` | `/retailers/item/remove/<int:item_id>` | Remove an inventory item (batch)                                             | Retailer Req.     |
| `POST`   | `/retailers/inventory/<int:id>/sell` | Sell quantity from an inventory item                                         | Retailer Req.     |
| `POST`   | `/retailers/inventory/<int:id>/list` | Change item status to 'Listing'                                              | Retailer Req.     |
| `GET`    | `/retailers/notifications`     | Get notifications for the authenticated retailer                             | Retailer Req.     |
| `GET`    | `/retailers/requests`          | Get requests from NGOs for the retailer's food                               | Retailer Req.     |
| `POST`   | `/retailers/requests/<int:request_id>/approve` | Approve an NGO's request                                                     | Retailer Req.     |
| `POST`   | `/retailers/requests/<int:request_id>/ignore` | Ignore an NGO's request                                                      | Retailer Req.     |
| `POST`   | `/retailers/food/<int:id>/ignore` | Ignore notification for an item                                              | Retailer Req.     |
| `GET`    | `/farmer/simple_demand_forecast` | Get simple demand forecast and market analysis based on recent regional data | Farmer Required   |


## Project Structure
```
.
├── foodloop_app
│   ├── api_docs.md
│   ├── auth_routes.py
│   ├── farmer_routes.py
│   ├── food_routes.py
│   ├── __init__.py
│   ├── models.py
│   ├── ngo_routes.py
│   └── retailer_routes.py
├── requirements.txt
└── run.py

```



## Contributing

Contributions are welcome, especially as this was a hackathon project! If you have suggestions for improvements, bug fixes, or new features, please open an issue or submit a pull request.


## Acknowledgments

* Grateful for the capabilities provided by the Google Gemini API.
* Shoutout to the Flask and SQLAlchemy communities for their excellent documentation and support.

