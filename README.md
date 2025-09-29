<h1>ExpNo 1 :Developing AI Agent with PEAS Description</h1>
<h3>Name: VASUKANNAN R </h3>
<h3>Register Number:212224080060 </h3>


<h3>AIM:</h3>
<br>
<p>To find the PEAS description for the given AI problem and develop an AI agent.</p>
<br>
<h3>Theory</h3>
<h3>Medicine prescribing agent:</h3>
<p>Such this agent prescribes medicine for fever (greater than 98.5 degrees) which we consider here as unhealthy, by the user temperature input, and another environment is rooms in the hospital (two rooms). This agent has to consider two factors one is room location and an unhealthy patient in a random room, the agent has to move from one room to another to check and treat the unhealthy person. The performance of the agent is calculated by incrementing performance and each time after treating in one room again it has to check another room so that the movement causes the agent to reduce its performance. Hence, agents prescribe medicine to unhealthy.</p>
<hr>
<h3>PEAS DESCRIPTION:</h3>
<table>
  <tr>
    <td><strong>Agent Type</strong></td>
    <td><strong>Performance</strong></td>
     <td><strong>Environment</strong></td>
    <td><strong>Actuators</strong></td>
    <td><strong>Sensors</strong></td>
  </tr>
    <tr>
    <td><strong>Medicine prescribing agent</strong></td>
    <td><strong>Treating unhealthy, agent movement</strong></td>
     <td><strong>Rooms, Patient</strong></td>
    <td><strong>Medicine, Treatment</strong></td>
    <td><strong>Location, Temperature of patient</strong></td>
  </tr>
</table>
<hr>
<H3>DESIGN STEPS</H3>
<h3>STEP 1:Identifying the input:</h3>
<p>Temperature from patients, Location.</p>
<h3>STEP 2:Identifying the output:</h3>
<p>Prescribe medicine if the patient in a random has a fever.</p>
<h3>STEP 3:Developing the PEAS description:</h3>
<p>PEAS description is developed by the performance, environment, actuators, and sensors in an agent.</p>
<h3>STEP 4:Implementing the AI agent:</h3>
<p>Treat unhealthy patients in each room. And check for the unhealthy patients in random room</p>
<h3>STEP 5:</h3>
<p>Measure the performance parameters: For each treatment performance incremented, for each movement performance decremented</p>

# Step 1 & 2: Inputs and outputs handled in environment
class HospitalEnvironment:
    def __init__(self, rooms=3):
        # Each room has a patient with random temperature
        self.rooms = {f"Room{i+1}": random.randint(97, 103) for i in range(rooms)}
        self.agent_location = "Room1"
        self.performance = 0

    def is_patient_sick(self):
        return self.rooms[self.agent_location] >= 100  # fever if temp ≥ 100

    def treat(self):
        if self.is_patient_sick():
            self.rooms[self.agent_location] = 98  # reset temperature (treated)
            self.performance += 10
        else:
            self.performance -= 1  # unnecessary treatment

    def move(self):
        # move randomly to another room
        self.agent_location = random.choice(list(self.rooms.keys()))
        self.performance -= 1

    def status(self):
        return f"Location: {self.agent_location}, Rooms: {self.rooms}, Score: {self.performance}"


# Step 4: Agent
class DoctorAgent:
    def program(self, env):
        if env.is_patient_sick():
            return "TREAT"
        else:
            return "MOVE"

# Step 5: Run simulation
env = HospitalEnvironment(rooms=3)
agent = DoctorAgent()

print("Initial:", env.status())
for step in range(8):
    action = agent.program(env)
    if action == "TREAT":
        env.treat()
    else:
        env.move()
    print(f"Step {step+1}: Action={action} -> {env.status()}")

print("\nFinal Score:", env.performance)
ouput<img width="1920" height="757" alt="EXP1AI OP" src="https://github.com/user-attachments/assets/bd94ac4f-3f93-4ab3-81e1-5d7dfa1647b9" />
