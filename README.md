Mean-Variance-Standard Deviation Calculator

This project implements a Python function that calculates various statistical properties (mean, variance, standard deviation, max, min, and sum) for a 3x3 matrix derived from a list of nine numbers. The calculations are performed for the rows, columns, and the flattened matrix.FeaturesThe calculate function takes a list of 9 numbers and returns a dictionary containing the following statistics:Mean: Calculated for columns, rows, and the flattened matrix.Variance: Calculated for columns, rows, and the flattened matrix.Standard Deviation: Calculated for columns, rows, and the flattened matrix.Max: The maximum value for columns, rows, and the flattened matrix.Min: The minimum value for columns, rows, and the flattened matrix.Sum: The sum of values for columns, rows, and the flattened matrix.If the input list does not contain exactly nine numbers, a ValueError is raised.SetupTo run this project, you'll need Python and the NumPy library installed.PrerequisitesPython 3.xpip (Python package installer)InstallationClone the repository (if applicable) or create the project files:If you're working in a Codespace, you likely already have the files. Otherwise, ensure you have the following files in your project directory:mean_var_std.pymain.pytest_module.py (optional, for running tests)Install NumPy:Open your terminal or command prompt and run:pip install numpy
Usagemean_var_std.py

This file contains the core calculate function.

import numpy as np

def calculate(list_of_nine_numbers):
    """
    Calculates mean, variance, standard deviation, max, min, and sum
    for rows, columns, and the flattened 3x3 NumPy array created from
    the input list.

    Args:
        list_of_nine_numbers: A list containing exactly nine numbers.

    Returns:
        A dictionary containing the calculated statistics.

    Raises:
        ValueError: If the input list does not contain nine numbers.
    """
    if len(list_of_nine_numbers) != 9:
        raise ValueError("List must contain nine numbers.")

    np_array = np.array(list_of_nine_numbers).reshape(3, 3)

    mean_columns = np_array.mean(axis=0).tolist()
    mean_rows = np_array.mean(axis=1).tolist()
    mean_flat = np_array.mean()

    var_columns = np_array.var(axis=0).tolist()
    var_rows = np_array.var(axis=1).tolist()
    var_flat = np_array.var()

    std_columns = np_array.std(axis=0).tolist()
    std_rows = np_array.std(axis=1).tolist()
    std_flat = np_array.std()

    max_columns = np_array.max(axis=0).tolist()
    max_rows = np_array.max(axis=1).tolist()
    max_flat = np_array.max()

    min_columns = np_array.min(axis=0).tolist()
    min_rows = np_array.min(axis=1).tolist()
    min_flat = np_array.min()

    sum_columns = np_array.sum(axis=0).tolist()
    sum_rows = np_array.sum(axis=1).tolist()
    sum_flat = np_array.sum()

    calculations = {
        'mean': [mean_columns, mean_rows, mean_flat],
        'variance': [var_columns, var_rows, var_flat],
        'standard deviation': [std_columns, std_rows, std_flat],
        'max': [max_columns, max_rows, max_flat],
        'min': [min_columns, min_rows, min_flat],
        'sum': [sum_columns, sum_rows, sum_flat]
    }

    return calculations
main.pyThis file serves as an entry point to demonstrate the calculate function and can be used to run your unit tests.import mean_var_std
from unittest import main

# Example usage of your calculate function
try:
    result = mean_var_std.calculate([0,1,2,3,4,5,6,7,8])
    print("Calculations for [0,1,2,3,4,5,6,7,8]:")
    print(result)
except ValueError as e:
    print(f"Error: {e}")

# Run unit tests automatically (if test_module.py exists)
# main(module='test_module', exit=False)
To run the main.py script, navigate to your project directory in the terminal and execute:python main.py
You will see the calculated statistics printed to the console.TestingThe project includes a test_module.py file for unit testing
the calculate function.test_module.py (Example)import unittest

import mean_var_std # Import your module

class UnitTests(unittest.TestCase):
  
    def test_calculate_function_valid_input(self):
        # Test case for valid input
        input_list = [0, 1, 2, 3, 4, 5, 6, 7, 8]
        expected_mean_flat = 4.0
        result = mean_var_std.calculate(input_list)
        self.assertAlmostEqual(result['mean'][2], expected_mean_flat)
        # Add more specific assertions for rows, columns, and other stats

    def test_calculate_function_invalid_input_length(self):
        # Test case for incorrect input length
        with self.assertRaises(ValueError) as cm:
            mean_var_std.calculate([1, 2, 3])
        self.assertEqual(str(cm.exception), "List must contain nine numbers.")

    def test_calculate_function_another_valid_input(self):
        input_list = [9, 8, 7, 6, 5, 4, 3, 2, 1]
        result = mean_var_std.calculate(input_list)
        self.assertAlmostEqual(result['mean'][2], 5.0)
        self.assertEqual(result['sum'][0], [18, 15, 12]) # Sum of columns [9+6+3, 8+5+2, 7+4+1]
        self.assertEqual(result['sum'][1], [24, 15, 6]) # Sum of rows [9+8+7, 6+5+4, 3+2+1]


if __name__ == '__main__':
    unittest.main()
To run the unit tests, ensure the main(module='test_module', exit=False) line in main.py is uncommented, or simply run test_module.py directly:python -m unittest test_module.py
