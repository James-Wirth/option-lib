# OptionLib

OptionLib is a C++ library designed for options pricing and financial modelling, with support for various pricing models. This project is a **work in progress**, with more features planned for future release.

## Features

- **Pricing models**
  - Black-Scholes
  - Monte-Carlo
  - Binomial model
  - More soon...!

- **Portfolio management**
  - Create and manage a portfolio of options
  - Greek sensitivity analysis
 
## Installation

Make sure you have a C++20 compatible compiler. Clone the repo and build using CMake:

```bash
git clone https://github.com/James-Wirth/OptionLib.git
cd OptionLib
mkdir build && cd build
cmake ..
make
```

## Usage

Here is a simple usage that demonstrates setting up a portfolio with call and put options:

```cpp
using namespace OptionLib;

// Black-Scholes model with spot 100.0, risk-free rate 0.05
// and constant volatility 0.2
auto model = Factory::createModel<BlackScholes>(100.0, 0.05, 0.2);

// Instantiate portfolio with default model type <BlackScholes>
Portfolio portfolio(model);

// Create a call option with strike 100.0, expiry 1.0
auto callOption = Factory::createOption(100.0, 1.0, OptionType::Call);

// Add option to the portfolio
portfolio.addOption(callOption);
```

Calculate the Greeks for the portfolio:

```cpp
auto greekVector = portfolio.greekVector(GreekType::Delta)
```

Calculate the portfolio value:

```cpp
double portfolioValue = portfolio.totalValue()
```

Calculate the risk profile of the portfolio:

```cpp
// Value at risk with 95% confidence and a holding period of 1/52
double portfolioVaR = portfolio.VaR(0.95, 1.0/52);

// Expected shortfall with 95% confidence and holding period of 1/52
double portfolioES = portfolio.ExpectedShortfall(0.95, 1.0/52);
```



