# Movie Tickets Management System
We have decided to make a database about movie
tickets and theatres by looking at the craze in the 
public towards Indian cinemas.
A movie ticket database is a collection of information
regarding movie tickets that have been sold or
reserved. It includes information such as the movie 
title, showtime, theatre location, ticket price, seat 
number, and customer information. This information 
can be used to manage the number of tickets sold , 
track attendance, payment transactions and analyse 
customer behaviour. The database can be stored in a
computer system which reduces the work load on 
humans.

Sure, here's a Python example of a `tkinter` UI that allows users to upload an Excel file, perform a machine learning prediction, and then display the results. This example assumes you have a pre-trained machine learning model ready to use.

First, install the necessary libraries if you haven't already:

```sh
pip install pandas openpyxl scikit-learn
```

Here's the complete code:

```python
import tkinter as tk
from tkinter import filedialog, messagebox
import pandas as pd
from io import BytesIO
from sklearn.externals import joblib  # Replace with your actual import for ML model

# Load your pre-trained machine learning model
# model = joblib.load('path_to_your_model.pkl')

# Function to make a prediction (Replace with your actual prediction code)
def make_prediction(data):
    # Example: Pretend we make a prediction using the data extracted
    # Replace this with your actual prediction logic
    predictions = {"ExampleColumn": ["Prediction 1", "Prediction 2", "Prediction 3"]}
    return pd.DataFrame(predictions)

# Function to handle file upload and processing
def upload_file():
    file_path = filedialog.askopenfilename(filetypes=[("Excel files", "*.xlsx")])
    if file_path:
        try:
            # Read Excel file
            input_df = pd.read_excel(file_path)
            
            # Perform prediction
            prediction_df = make_prediction(input_df)
            
            # Convert DataFrame to Excel
            output = BytesIO()
            with pd.ExcelWriter(output, engine='xlsxwriter') as writer:
                prediction_df.to_excel(writer, index=False, sheet_name='Predictions')
                writer.save()
                processed_data = output.getvalue()
            
            # Save Excel file
            save_path = filedialog.asksaveasfilename(defaultextension=".xlsx", filetypes=[("Excel files", "*.xlsx")])
            if save_path:
                with open(save_path, 'wb') as f:
                    f.write(processed_data)
                messagebox.showinfo("Success", "Predictions saved successfully!")
            else:
                messagebox.showwarning("Save Cancelled", "Save operation was cancelled.")
            
            # Display predictions in the text box
            result_text.delete("1.0", tk.END)
            result_text.insert(tk.END, prediction_df.to_string(index=False))
            
        except Exception as e:
            messagebox.showerror("Error", str(e))
    else:
        messagebox.showwarning("No File Selected", "Please select an Excel file.")

# Set up the main tkinter window
root = tk.Tk()
root.title("Excel Prediction App")
root.geometry("600x400")

# Create and place widgets
upload_button = tk.Button(root, text="Upload Excel", command=upload_file)
upload_button.pack(pady=20)

result_text = tk.Text(root, wrap=tk.WORD, height=15, width=70)
result_text.pack(pady=20)

# Run the tkinter main loop
root.mainloop()
```

### Explanation:

1. **Import Libraries**: Import the necessary libraries, including `tkinter`, `pandas`, and `joblib` for loading the machine learning model.
2. **Load ML Model**: Load your pre-trained machine learning model. Replace the placeholder with the actual path to your model.
3. **Make Prediction**: Define a function to make predictions using the input data. Replace the example prediction logic with your actual model's prediction logic.
4. **File Upload and Processing**:
   - Use `filedialog.askopenfilename` to open a file dialog for selecting the Excel file.
   - Read the selected Excel file into a DataFrame using `pd.read_excel`.
   - Perform predictions using the input DataFrame.
   - Convert the prediction results to an Excel file and save it.
   - Display the prediction DataFrame in a `tkinter` Text widget.
5. **Set up the tkinter Window**: Create the main window, add a button for uploading the Excel file, and a text widget to display the results.
6. **Run the tkinter Main Loop**: Start the tkinter main loop to run the application.

This example provides a basic workflow and can be further customized based on your specific requirements. Ensure you replace the placeholder prediction logic with your actual machine learning model and prediction code.
