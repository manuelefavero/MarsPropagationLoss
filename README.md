# Mars Propagation Loss Model in ns-3

This repository contains a customized propagation loss model implementation for the ns-3 network simulator, designed specifically for simulating the unique propagation conditions on Mars. This includes attenuation due to Martian dust storms and other environmental factors. The repository also includes an example to test and simulate network scenarios using the Mars Propagation Loss Model.

## Key Components

### 1. `MarsPropagationLossModel`
The `MarsPropagationLossModel` extends the `PropagationLossModel` in ns-3 and introduces the following features:

- **Path Loss Exponent:** Configurable parameter to adjust the rate of power decay over distance.
- **Dust Particle Attenuation:** Incorporates attenuation caused by Martian dust particles. Calculations include:
  - Particle density (`N_T`)
  - Mean particle radius (`r`)
  - Dielectric permittivity of particles (real and imaginary parts)
- **Wavelength Dependency:** Takes into account the signal wavelength (`lambda`) for attenuation and propagation loss calculations.

#### Attributes and Methods
- **Setters:**
  - `SetPathLossExponent(double n)`
  - `SetDistance(double n)`
  - `SetN_T(double n)`
  - `SetParticleRadius(double n)`
  - `SetEpsilonReal(double n)`
  - `SetEpsilonImm(double n)`
  - `SetLambda(double n)`

- **Getters:**
  - `GetPathLossExponent()`
  - `GetDistance()`
  - `GetN_T()`
  - `GetParticleRadius()`
  - `GetEpsilonReal()`
  - `GetEpsilonImm()`
  - `GetLambda()`

- **Simulation:**
  - Implements `DoCalcRxPower()` to calculate the received power based on the Mars-specific propagation conditions.

### 2. `mars-simulation-example.cc`
A sample ns-3 simulation script to test the throughput of Aloha protocol-based communication in Mars-like conditions using LoRaWAN. This file demonstrates how the Mars Propagation Loss Model integrates with existing ns-3 scenarios.

### 3. Base Files
The repository includes the source (`.cc`) and header (`.h`) files for defining and implementing the Mars Propagation Loss Model.

## Installation
1. Clone this repository:
   ```bash
   git clone <https://github.com/manuelefavero/MarsPropagationLoss>
   ```
2. Copy the `propagation-loss-model.cc` and `propagation-loss-model.h` files into the appropriate ns-3 directory (e.g., `src/propagation/model`).
3. Add the `MarsPropagationLossModel` to the ns-3 build system by updating the `wscript` in the `src/propagation` folder.
4. Rebuild ns-3:
   ```bash
   ./waf configure
   ./waf build
   ```

## Usage
- Include the `MarsPropagationLossModel` in your ns-3 simulation scripts:
  ```cpp
  #include "ns3/propagation-loss-model.h"
  ```
- Instantiate and configure the model in your simulation:
  ```cpp
  Ptr<MarsPropagationLossModel> marsLoss = CreateObject<MarsPropagationLossModel>();
  marsLoss->SetPathLossExponent(3);
  marsLoss->SetN_T(8e7);
  marsLoss->SetParticleRadius(3e-6);
  marsLoss->SetEpsilonReal(2.9038);
  marsLoss->SetEpsilonImm(0.1278);
  marsLoss->SetLambda(299792458.0/868e-6);
  ```

## Authors
- **Alessandro Canova**
- **Manuele Favero**

## License
This project is licensed under the GNU General Public License v2. See the LICENSE file for details.

## References
- [ns-3 Documentation](https://www.nsnam.org/documentation/)
- [LoRaWAN ns-3 Module](https://github.com/signetlabdei/lorawan)
- Research on Martian dust storm propagation effects.

## Contributing
Feel free to submit issues or contribute to the development of this module by creating pull requests.
