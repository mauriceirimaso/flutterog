# flutterog



void main() {
  // Sample list of item prices
  List<double> itemPrices = [50.0, 25.0, 5.0, 15.0, 100.0];

  // Define a tax rate (optional parameter for calculateTotal)
  double taxRate = 0.1; // 10%

  // Step 1: Filter out items below a threshold (using anonymous function)
  double threshold = 10.0;
  List<double> filteredItems = itemPrices.where((price) => price >= threshold).toList();
  print('Filtered items (above \$$threshold): $filteredItems');

  // Step 2: Apply discount using higher-order function
  double discountPercentage = 0.2; // 20%
  List<double> discountedPrices = applyDiscount(filteredItems, (price) => price * (1 - discountPercentage));
  print('Prices after discount: $discountedPrices');

  // Step 3: Calculate total with tax
  double totalPrice = calculateTotal(discountedPrices, taxRate: taxRate);
  print('Total price with tax: \$${totalPrice.toStringAsFixed(2)}');

  // Step 4: Calculate special factorial discount based on the number of items
  double factorialDiscount = calculateFactorialDiscount(discountedPrices.length) / 100;
  double finalPrice = totalPrice * (1 - factorialDiscount);
  print('Final price after applying factorial discount: \$${finalPrice.toStringAsFixed(2)}');
}

// Function to calculate the total price with an optional tax rate
double calculateTotal(List<double> prices, {double taxRate = 0.0}) {
  double total = prices.reduce((a, b) => a + b);
  return total * (1 + taxRate);
}

// Higher-order function to apply a discount to all prices
List<double> applyDiscount(List<double> prices, double Function(double) discountFunction) {
  return prices.map(discountFunction).toList();
}

// Recursive function to calculate factorial discount based on number of items
int calculateFactorialDiscount(int n) {
  if (n <= 1) return 1;
  return n * calculateFactorialDiscount(n - 1);
}
