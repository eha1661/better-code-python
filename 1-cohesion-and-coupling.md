# Cohesion and Coupling

## What are cohesion and coupling?

Cohesion and coupling are two concepts that measure how well your classes and modules are designed and related to each other. In other words, they are metrics to measure the software quality.

**Cohesion** refers to how strongly the elements of a class or module belong together and support a single purpose or responsibility. <br>Similarly, it refers to the degree to which the elements within a module or function are related to each other and work together to achieve a common purpose


**Coupling** refers to how much a class or module depends on or interacts with other classes or modules.

Ideally, you want high cohesion and low coupling in your design, as this makes your code easier to understand, test, and modify.

## Cohesion

Let's take this example:

``` python
class DataProcessor:
def __init__(self, data):
    self.data = data

def preprocess_data(self):
    # Preprocessing code that removes duplicates
    pass

def analyze_data(self):
    # Analyzing code that calculates statistics
    pass

def visualize_data(self):
    # Visualization code that creates graphs
    pass

def export_data(self):
    # Exporting code that saves data to a file
    pass

def send_email_report(self):
    # Sending an email report
    pass
```

> In the above code, the DataProcessor class has multiple methods that perform different and unrelated tasks such as preprocessing, analyzing, visualizing, exporting, and sending email reports. These tasks have low cohesion because they don't share a common purpose, and combining them in a single class makes it difficult to understand and maintain the code.

To improve cohesion in the code, we refactor it into separate classes, each responsible for a specific task.

``` python
class DataPreprocessor:
    def __init__(self, data):
        self.data = data

    def preprocess_data(self):
        # Preprocessing code that removes duplicates
        pass

class DataAnalyzer:
    def __init__(self, data):
        self.data = data

    def analyze_data(self):
        # Analyzing code that calculates statistics
        pass

class DataVisualizer:
    def __init__(self, data):
        self.data = data

    def visualize_data(self):
        # Visualization code that creates graphs
        pass

class DataExporter:
    def __init__(self, data):
        self.data = data

    def export_data(self):
        # Exporting code that saves data to a file
        pass

class EmailReporter:
    def __init__(self, data):
        self.data = data

    def send_email_report(self):
        # Sending an email report
        pass
```

An other example of a function with low cohesion.

``` python
import requests
from bs4 import BeautifulSoup
import re

def scrape_and_clean(url):
    # Web scraping
    try:
        response = requests.get(url)
        if response.status_code == 200:
            soup = BeautifulSoup(response.content, 'html.parser')
            scraped_text = soup.get_text()
        else:
            print("Failed to fetch the webpage.")
            return
    except Exception as e:
        print(f"An error occurred while scraping: {str(e)}")
        return

    # Text cleaning
    cleaned_text = re.sub(r'\n+', '\n', scraped_text)  # Remove multiple newlines
    cleaned_text = re.sub(r'\s+', ' ', cleaned_text)   # Remove extra whitespace

    # Miscellaneous operations
    word_count = len(cleaned_text.split())
    if word_count > 1000:


        print("This is a long document.")
    else:
        print("This is a short document.")

    if 'important keyword' in cleaned_text:
        print("The document contains an important keyword.")

    # ... Other unrelated tasks ...

    return cleaned_text
```

> function is not cohesive because it combines several unrelated tasks within the same function. It has multiple responsibilities ...

## Coupling

``` python
def CheckEmailSecurity(email):
    if email.header.bearer.invalid():
        raise Exception("email header bearer is invalid")
    elif email.header.received =! email.header.received_spf:
        raise Exception("recieved mismatch")
    else:
        print("email header is secure")
```

> this funtion is highly coupled with the email object. access deep structures in the email object. Changing something in email structure will lead us to change all the function.

## Use Case

Problems in code [[coupling-cohesion-before.py](./code/coupling-cohesion-before.py))]

* `register_vehicle` does many things, it has week cohesion.
* add new brand means changing catalogue prices catalogue_prices (if brand ...) and changing taxe_percentage ...
* strong coupling between Application (register_vehicle) and VehicleRegistry

    ``` python
        def register_vehicle(self, brand: string):
            # create a registry instance
            registry = VehicleRegistry()

            # using details with VehicleRegistry methods
            vehicle_id = registry.generate_vehicle_id(12)

            # we pass the vehicle_id to the method generate_vehicle_license of VehicleRegistry
            license_plate = registry.generate_vehicle_license(vehicle_id)

            # changes in  VehicleRegistry => changes in class Application
    ```

Steps of refactoring:
* Where is the information that your application uses. How it is sstored and how you can access it.
* Structure the data in logical way and add the necessary information and methods to tackle

## 5 Tips To Achieve Low Coupling
TODO

## Resources

* `1`[ How do you apply the principles of cohesion and coupling to improve your design quality?](https://www.linkedin.com/advice/0/how-do-you-apply-principles-cohesion-coupling)
* `2`[ Cohesion and Coupling: Write BETTER PYTHON CODE Part 1](https://www.youtube.com/watch?v=eiDyK_ofPPM)
* `4` [use case source code](https://github.com/ArjanCodes/betterpython/tree/main/1%20-%20coupling%20and%20cohesion)
* `5` [5 Tips To Achieve Low Coupling In Your Python Code](https://www.youtube.com/watch?v=qR4-PBLUZNw&ab_channel=ArjanCodes)
* Applying UML and Patterns: An Introduction to Object-Oriented Analysis and Design and Iterative Development, by Craig Larman
