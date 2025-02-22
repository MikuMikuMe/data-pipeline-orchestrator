# data-pipeline-orchestrator

Creating a Python program for a data pipeline orchestrator to automate and optimize ETL workflows involves several key components: extracting data from sources, transforming it, and loading it into a destination. Here is a simple Python program that outlines these steps. This example focuses on a scenario where data is extracted from a file or database, transformed, and then loaded into another system, like a database or file.

This program will include basic error handling and comments for clarity. Note that in a real-world scenario, you'd integrate specific libraries for interacting with databases, cloud services, or other data sources/destinations, such as SQLAlchemy, pandas, etc. For simplicity, this code uses basic Python and assumes CSV file data sources and targets.

```python
import os
import pandas as pd

# ETL process orchestrator
class DataPipelineOrchestrator:
    def __init__(self, source_file, destination_file):
        """
        Initialize the orchestrator with source and destination paths.
        """
        self.source_file = source_file
        self.destination_file = destination_file

    def extract(self):
        """
        Extract data from the source.
        """
        try:
            if not os.path.exists(self.source_file):
                raise FileNotFoundError(f"The source file {self.source_file} does not exist.")
            
            # Reading data from CSV (a placeholder for any data extraction logic)
            data = pd.read_csv(self.source_file)
            print(f"Successfully extracted data from {self.source_file}")
            return data
        except Exception as e:
            print(f"Error during extraction: {str(e)}")
            raise

    def transform(self, data):
        """
        Transform the data as needed.
        """
        try:
            # Placeholder transformation: drop rows with any missing values
            transformed_data = data.dropna()
            print("Data transformation complete.")
            return transformed_data
        except Exception as e:
            print(f"Error during transformation: {str(e)}")
            raise

    def load(self, data):
        """
        Load transformed data into the destination.
        """
        try:
            # Writing transformed data to CSV (a placeholder for any data loading logic)
            data.to_csv(self.destination_file, index=False)
            print(f"Successfully loaded data into {self.destination_file}")
        except Exception as e:
            print(f"Error during loading: {str(e)}")
            raise

    def run_pipeline(self):
        """
        Run the full ETL process: extract, transform, and load.
        """
        try:
            print("Starting ETL pipeline...")
            data = self.extract()
            transformed_data = self.transform(data)
            self.load(transformed_data)
            print("ETL pipeline completed successfully.")
        except Exception as e:
            print(f"Pipeline execution failed: {str(e)}")

# To use the DataPipelineOrchestrator, initialize it with source and destination paths
if __name__ == "__main__":
    # Example usage with a CSV source and destination
    source_file = 'source_data.csv'
    destination_file = 'transformed_data.csv'

    orchestrator = DataPipelineOrchestrator(source_file, destination_file)
    orchestrator.run_pipeline()
```

### Key Points:
- **Error Handling**: Each stage of the extract-transform-load (ETL) process has a try-except block to catch and print errors.
- **Modularity**: The program is organized into separate methods for extraction, transformation, and loading.
- **Logging**: Print statements are used to log progress and errors. In a production environment, consider using Python's `logging` module for more control over log levels and outputs.
- **Assumptions**: This example assumes the data is in CSV format and uses basic transformation (dropping rows with missing data). You'll need to adjust it for different sources, destinations, or transformation logic based on your specific requirements.

This simple orchestrator provides a foundation for more sophisticated ETL pipelines which could integrate with APIs, handle various data formats, or be scheduled to run regularly.