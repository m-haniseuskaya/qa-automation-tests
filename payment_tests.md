# Payment Feature Test Cases

## Test Case 1: Valid Payment
- Input: Card number valid, amount valid
- Expected: Payment successful, confirmation shown
- Status: Ready for automation

## Test Case 2: Declined Card
- Input: Declined card, amount valid
- Expected: Error message shown
- Status: Ready for automation

## Test Case 3: Expired Card
- Input: Expired card, amount valid
- Expected: Declined, error "Card expired"
- Status: Ready for automation

## Test Case 4: Zero Amount
- Input: Amount = 0
- Expected: Validation error "Amount must be greater than 0"
- Status: Ready for automation