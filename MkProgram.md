#### **1. Check infrastructure readiness**
- docker-compose
- JMeter
- proxy

#### **2. Describe the deployed infrastructure**
- Components
- Architecture
- Purpose of each part

#### **3. Open JMeter**
- Add a Thread Group
  - Say a few words about what it is
- Start the Test Script Recorder
- Record a scenario
- Analyze each recorded element in detail:
  - Samples
  - Header Manager
  - Add Debug Sampler

#### **4. Start unifying the scenario**
- Install the Plugin Manager
- Add elements: 
  - Custom Thread Group
  - View Results Tree
  - Backend Listener
  - CSV Data Set Config
  - HTTP Request Defaults
  - User Defined Variables
  - Header Manager
- Run the scenario, make sure it works, check the results
- Work with Header Manager inside each request
- Use JSON Extractor
- Work with JSR223 Pre/Post Processor

#### **5. Generate the first perf report**
- Add Ultimate Thread Group with parameters: 100 0 300 0 0
- Say a few words about it
- Simulate load with a ramp-up shape
- Disable recording and debug tools
- Build a command to run the test and generate the report
- While the test is running (approx. 10 min), collect feedback
- Analyze the generated report