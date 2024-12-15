# Polls Haven Project

## Overview
Polls Haven is a Django-powered web application designed for managing and collecting survey data by allowing users to participate in polls, manage their subscriptions, and handle payments securely. It provides functionalities like user authentication, subscription plans, dynamic forms, polling, and analytics. The project is structured to handle multiple apps for better scalability and maintainability, ensuring a seamless user experience.

## Features
1. **User Authentication and Registration**
   - Users can register using a custom user registration form.
   - The registration form includes fields like username, email, and password.
   - After registration, users are automatically logged in and redirected to the home page.
   - Login, logout, and password change functionality.

2. **Login and Logout**
   - Users can log in using their registered credentials.
   - The login form is styled and designed to match the application’s theme.
   - Users can log out securely, redirecting them to the login page if they are not authenticated.

3. **Poll Management**
   - Users can view and participate in various polls.
   - Questions are displayed in a structured format with voting functionality.
   - Polls are ordered by the most recent publication date.

4. **Subscription Management**
   - Users can view available subscription plans and manage their subscriptions.
   - Trial, free, and premium plans with varying access to features.
   - Admin users can send notifications related to subscriptions.

5. **Payments Integration**
   - Payment forms are integrated to handle secure payment processing.
   - Redirect users to payment pages for processing transactions.
   
6. **User Dashboard**
   - Authenticated users have access to a personalized dashboard.
   - Dashboard includes links to poll participation, subscription management, and logout.

7. **Navbar and Footer** 
   - Responsive navbar for navigation, including links for logged-in and non-logged-in users.
   - Footer providing relevant information and links.

8. **Custom Templates and Styling**
   - Custom user interface templates for registration, login, and user dashboard.
   - Styled using Bootstrap for a modern, responsive design.

9. **Error Handling and Redirects**
   - Middleware ensures unauthenticated users are redirected to login.
   - Custom error pages for authentication and unauthorized access.

10. **Dynamic Polls**
   - Create, update, and view polls with multiple-choice and open-ended questions.
     
11. **Reporting & Analytics**
   - Admin dashboard for managing subscriptions, payments, and analytics.
     
12. **Responsive UI**
   - Bootstrap-based templates for a modern, aesthetic look.
     
13. **M-Pesa Integration**
   - Payment collection using M-Pesa Daraja API.


## Setup Instructions

### Prerequisites
- Virtualenv (optional for managing dependencies)
- Python 3.12.6 or later
- Django 5.0.2 or later
- MySQL database (version 8.0 or later)
- M-Pesa Daraja API access (for payment gateway)
- Docker (optional for containerization)

### Installation

#### Step 1: Clone the repository
```bash
git clone https://github.com/OumaCavin/polls-haven-plus.git
cd polls-haven-plus
```

#### Step 2: Set up a virtual environment
```bash
python -m venv polls_haven_env
source polls_haven_env/bin/activate   # On Linux/Mac
.\polls_haven_env\Scripts\activate    # On Windows
```

#### Step 3: Install dependencies
```bash
pip install -r requirements.txt
```

#### Step 4: Configure the database
Edit `settings.py`:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'polls_haven_db',  # Change this to your desired database name
        'USER': 'your_db_user',
        'PASSWORD': 'your_db_password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

#### Step 5: Migrate the database
```bash
python manage.py migrate
```

#### Step 6: Create admin superuser
```bash
python manage.py createsuperuser
```

#### Step 7: Run the development server
```bash
python manage.py runserver
```

#### Step 8: Access the application at `http://127.0.0.1:8000/`.

## Project Structure

```plaintext
PollsHaven/
├── polls/                           # Main app handling polls and forms
│   ├── migrations/
│   │   ├── __init__.py
│   ├── static/                     # Static files (CSS, JS, images)
│   │   ├── polls/
│   │       ├── css/
│   │       ├── js/
│   │       └── images/
│   ├── templates/                    # Templates for frontend
│   │   ├── polls/
│   │       ├── index.html
│   │       ├── detail.html
│   │       └── results.html
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── forms.py                    # Custom form handling (for subscriptions & polls)
│   ├── models.py                   # Database models
│   ├── urls.py                     # URLs configuration for the polls app
│   └── views.py                    # View functions
├── subscriptions/                  # App for managing subscription plans
│   ├── migrations/
│   │   ├── __init__.py
│   ├── static/                     # Static files for subscription UI
│   │   ├── polls/
│   │       ├── css/
│   │       ├── js/
│   │       └── images/
│   ├── templates/                    # Templates for subscription management
│   │   ├── subscriptions/
│   │       ├── subscription_list.html
│   │       └── subscription_success.html
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py                   # Models for subscription plans & transactions
│   ├── decorators.py
│   ├── management/
│       ├── commands/
│           ├── __init__.py
│           └── seed_subscription_plans.py
│   ├── urls.py                     # URLs configuration for subscription plans
│   └── views.py                    # View functions for handling subscriptions
├── payments/                        # App for handling payment integrations
│   ├── migrations/
│   │   ├── __init__.py
│   ├── templates/                   # Templates for payment management
│   │   ├── payments/
│   │       ├── payment_success.html
│   │       └── payment_failed.html
│   ├── static/
│   │   ├── payments/
│   │       ├── css/
│   │       ├── js/
│   │       └── images/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── forms.py                    # Forms for payment details (M-Pesa Daraja API)
│   ├── models.py                   # Payment transaction models
│   ├── urls.py                     # URLs for payment handling
│   └── views.py                    # View functions for processing payments
├── migrations/                      # Database migrations
├── static/                          # General static files (common across all apps)
│   ├── css/
│   ├── js/
│   ├── images/
├── templates/                       # Global templates (base templates, etc.)
│   ├── base_generic.html
│   ├── registration/
│   │   ├── login.html
│   │   ├── logout.html
│   │   ├── password_reset_form.html
│   │   ├── password_reset_done.html
│   │   ├── password_reset_confirm.html
│   │   ├── password_reset_complete.html
│   └── 404.html
├── polls_haven_plus/                 # My Project 
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   ├── wsgi.py
│   ├── middleware.py
├── media/                           # Media files (uploaded files like images)
├── README.md                        # This file
├── manage.py                        # Django management utility
└── requirements.txt                 # List of project dependencies
```

## Configuration

### 1. **Settings Configuration**
   - `settings.py` contains all necessary configurations like database, installed apps, middleware, and M-Pesa Daraja API credentials.
   
### 2. **M-Pesa Daraja API Configuration**
   - Register for M-Pesa Daraja API from Safaricom.
   - Add M-Pesa credentials in `settings.py` under `MPESA_DARAJA` section:
   
```python
MPESA_DARAJA = {
    'CONSUMER_KEY': 'your_consumer_key',
    'CONSUMER_SECRET': 'your_consumer_secret',
    'SHORTCODE': 'your_shortcode',
    'PASSKEY': 'your_passkey',
    'INITIATOR_NAME': 'your_initiator_name',
    'RESPONSE_TYPE': 'Completed',
}
```

### 3. **Subscription Plans Configuration**
   - Add subscription plan models in `sub_plans/models.py`:
   
```python
from django.db import models
from django.utils.timezone import now

class SubscriptionPlan(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
    duration = models.IntegerField(help_text="Duration in days/months/years")
    features = models.TextField()  # List of features

    def __str__(self):
        return self.name
```

### 4. **Admin Interface for Subscriptions and Payments**
   - Register the models in `sub_plans/admin.py` and `payments/admin.py`:
   
```python
from django.contrib import admin
from .models import SubscriptionPlan, PaymentTransaction

admin.site.register(SubscriptionPlan)
admin.site.register(PaymentTransaction)
```

### 5. **Payment Integration using M-Pesa Daraja API**
   - In `payments/views.py`, handle the payment logic:
   
```python
from django.shortcuts import render, redirect
from .forms import PaymentForm
from .models import PaymentTransaction
from .mpesa_daraja import MpesaDarajaClient  # Your custom MPESA Daraja client

def initiate_payment(request, subscription_id):
    subscription = SubscriptionPlan.objects.get(id=subscription_id)
    form = PaymentForm(request.POST or None)
    
    if form.is_valid():
        # Process payment using M-Pesa Daraja API
        mpesa_client = MpesaDarajaClient()
        response = mpesa_client.request_stk_push(
            amount=subscription.price,
            phone_number=form.cleaned_data['phone_number'],
            description=f"Payment for {subscription.name}"
        )
        
        if response['response_code'] == '0':
            # Save payment details
            PaymentTransaction.objects.create(
                subscription=subscription,
                phone_number=form.cleaned_data['phone_number'],
                amount=subscription.price,
                transaction_id=response['transaction_id'],
                status='pending'
            )
            return redirect('payment_success')
        else:
            # Handle payment failure
            return redirect('payment_failed')
    return render(request, 'payments/initiate_payment.html', {'form': form})
```

### 6. **Reporting and Analytics Integration**
   - Use Django Admin interface to view payment and subscription analytics.
   - Generate custom reports in `admin.py` or custom management commands.

---

## Usage
1. **Registration**: 
   - Navigate to `/register/` to create a new user account.
   - Fill out the registration form and submit to log in automatically.

2. **Login**: 
   - Visit `/login/` to log in using your credentials.
   - After logging in, you’ll be redirected to the dashboard.

3. **Polls**:
   - Navigate to `/polls/` to view available polls.
   - Participate by voting on polls.

4. **Subscriptions**:
   - Access subscription management at `/subscriptions/`.
   - Manage your subscriptions or view plans.

5. **Payments**:
   - Visit `/payments/` for payment-related functionalities.
   - Secure payment processing for subscriptions.

6. **Logout**:
   - Click on the Logout link in the navbar to log out.

## Contributing
Contributions are welcome! Please follow these guidelines:
1. Fork the repository.
2. Create a new branch: `git checkout -b feature-name`.
3. Commit your changes: `git commit -m 'Add feature: ...'`.
4. Push to the branch: `git push origin feature-name`.
5. Submit a pull request.
   
### **Source code**

To learn more about the Polls Haven Project check out my:

**[Project Source code](https://github.com/OumaCavin/polls-haven-plus)**.

## License
This project is licensed under the [MIT License](LICENSE).

