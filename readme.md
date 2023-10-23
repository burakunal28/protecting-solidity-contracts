# Solidity Bootcamp Task4

# How to Protect Against Solidity Underflow, Overflow, and Reentrancy Attacks?

## Underflow and Overflow:

- **Use Correct Data Types:** Limit variables with appropriate data types to ensure values stay within the expected range. For example:
    ```
    uint8 public myVariable; // Define the variable as uint8 to limit values between 0 and 255
    ```
- **Safe Mathematical Operations:** Safely perform mathematical operations using security libraries like `SafeMath`:
    ```
    // Use SafeMath for uint256 to prevent overflows and underflows
    using SafeMath for uint256;
    
    // Safe addition function
    function safeAddition(uint256 a, uint256 b) public pure returns (uint256) {
        return a.add(b);
    }
    ```

## Reentrancy Attacks:

- **Delay Ether Transfers:** Delay ether transfers until after other operations in the contract. For example:
    ```
    function transferAndDoSomething() public {
        // Other operations go here.

        // Ether transfer is placed last.
        recipient.transfer(amount);
    }
    ```
- **Control Gas Limits:** When making fund transfers, manually set gas limits for the fund transfer. For example:
    ```
    function transferFunds(address recipient, uint256 amount) public {
        // Other operations go here.

        // Manually set gas limit for the fund transfer.
        (bool success, ) = recipient.call{value: amount, gas: 20000}("");
        require(success, "Transfer failed");
    }
    ```

## Developer

This project was created by [Burak Ünal](https://linktr.ee/burakunal28).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
