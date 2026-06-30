# pythonandOpenCV

#Answer 1






#  input number 
option = int(input("Enter (1: Roll, 2: Pitch, 3: Yaw): "))

#  the user selected 1
if option == 1:
    # Print Roll 
    print(" Slow down left motors for left roll or right motors for right roll")
# Check 2
elif option == 2:
    # Print Pitch 
    print(" Slow down front motors or rear motors for pitch")

elif option == 3:
    #  Yaw 
    print(" Slow down diagonally opposite motors for yaw")










 #  Answer 2




 
 # drone's body weight
body_weight = float(input("Body weight : "))
# payload weight 
payload_weight = float(input("Payload weight: "))

#  add weights 
total_weight = body_weight + payload_weight
#  total weight 
print(f"Output: {total_weight:.2f} kg")

# Check total weight 
if total_weight > 2.0:
 print("Total weight is greater than 2 kg")
elif total_weight == 2.0:
 print("Total weight is equal to 2 kg")
else: print("Total weight is less than 2kg.")










#ans3





# problem
max_takeoff_weight = 4.5    # kg, float
frame_weight = 1.2          # kg, float
battery_weight = 0.8        # kg, float
num_propellers = 4          # int
motor_weight = 0.075        # kg per motor, float
is_gps_enabled = True       # bool
gps_module_weight = 0.05    # kg, float

#  base weight 
base_weight = frame_weight + battery_weight + (num_propellers * motor_weight) + gps_module_weight

#payload
max_payload = max_takeoff_weight - base_weight
#  calculated payload
print(f" Max payload: {max_payload} kg")

# 2. Print the data types 
print(" Variable Types:")
print("max_takeoff_weight:", type(max_takeoff_weight))
print("frame_weight:", type(frame_weight))
print("battery_weight:", type(battery_weight))
print("num_propellers:", type(num_propellers))
print("motor_weight:", type(motor_weight))
print("is_gps_enabled:", type(is_gps_enabled))
print("gps_module_weight:", type(gps_module_weight))

#  boolean variable r
can_carry_camera = max_payload >= 1.8
# Print the boolean 
print(f" Can carry 1.8kg camera: {can_carry_camera}")

# max takeoff weight in grams,
max_takeoff_grams = int(max_takeoff_weight * 1000)
# Print  gram value
print(f" Max takeoff weight in grams: {max_takeoff_grams}g")







#ans4





#  telemetry string 
telemetry = "DRONE_ID:PX4_001|ALT:120.5m|SPEED:18.3kmph|BATT:67%|STATUS:HOVERING|GPS:23.0225N,72.5714E"

# Split the string at every pipe '|' 
data = telemetry.split('|')

# 1. Extract values by splitting at ':' 
drone_id = data[0].split(':')[1]
# Remove 'm' and convert to float
alt = float(data[1].split(':')[1].replace('m', ''))
# Remove 'kmph' and convert to float
speed = float(data[2].split(':')[1].replace('kmph', ''))
# Remove '%' and convert to int
batt = int(data[3].split(':')[1].replace('%', ''))
# Extract status string
status = data[4].split(':')[1]
# Extract GPS string
gps = data[5].split(':')[1]
# 2. Check if the string "hover"  inside the lowercase 
is_hovering = "hover" in status.lower()
print(f"Is hovering: {is_hovering}")

# 3. Replace the specific word in the original string using the replace() method
telemetry_updated = telemetry.replace("HOVERING", "RETURNING_HOME")

# 4. Print the summary string
print(f"Summary: [{drone_id}] Alt: {alt}m | Batt: {batt}% | Coords: {gps}")









#Ans5 





#altitudes
altitudes = [0, 15, 42, 78, 120, 118, 115, 50, 20, 0]

# 1. Find the highest number in the list
max_alt = max(altitudes)
# Find the position where the highest number is located
max_second = altitudes.index(max_alt)
print(f"Max altitude {max_alt}m occurred at second {max_second}")

# 2. Calculate the average
avg_alt = sum(altitudes) / len(altitudes)
# Use :.2f in the f-string to round the float to 2 decimal places
print(f"Average altitude: {avg_alt:.2f}m")

# 3. Create an empty list to hold the altitude differences
climb_rates = []
# Loop from 0 up to the second-to-last item to prevent index errors
for i in range(len(altitudes) - 1):
    # Subtract current altitude from the next altitude
    rate = altitudes[i+1] - altitudes[i]
    # Add the result to our climb_rates list
    climb_rates.append(rate)

# 4. The highest positive rate is the steepest climb
steepest_climb = max(climb_rates)
# The lowest negative rate is the steepest descent
steepest_descent = min(climb_rates)
print(f"Steepest climb: {steepest_climb}m, Steepest descent: {steepest_descent}m")

# 5. Build a new list 
trimmed_path = [a for a in altitudes if a != 0]
print(f"Trimmed path: {trimmed_path}")















#ans6








waypoints = (
    ("WP1", 23.0225, 72.5714, 50),
    ("WP2", 23.0312, 72.5801, 80),
    ("WP3", 23.0401, 72.5900, 100),
    ("WP4", 23.0225, 72.5714, 0),
)

# 1. Use len() to count items in the tuple
print(f"Total waypoints: {len(waypoints)}")

# 2. Iterate through waypoints 
for name, lat, lon, alt in waypoints:
    print(f"{name}: Lat {lat}, Lon {lon}, Alt {alt}m")

# 3. Logic to find highest waypoint
highest_wp_name = ""
highest_alt = -1
# Loop through all waypoints
for name, lat, lon, alt in waypoints:
    # If the current altitude beats then update 
    if alt > highest_alt:
        highest_alt = alt
        highest_wp_name = name
print(f"Highest waypoint is {highest_wp_name} at {highest_alt}m")

# 4. Check if a specific waypoint exists in the tuple
target_wp = ("WP2", 23.0312, 72.5801, 80)
print(f"WP2 exists: {target_wp in waypoints}")

# 5. Try/Except block to catch the mutation error (tuples can't be changed)
try:
    # reassign an index value in a tuple triggers a TypeError
    waypoints[0][3] = 60
except TypeError:
    print("Waypoint data is immutable - mission integrity protected!")









    #ans7




# dictionary drone states
fleet = {
    "PX4_001": {"battery": 87, "altitude": 120, "status": "active", "payload_kg": 1.2},
    "PX4_002": {"battery": 23, "altitude": 0, "status": "grounded", "payload_kg": 0},
    "PX4_003": {"battery": 56, "altitude": 85, "status": "active", "payload_kg": 0.8},
    "PX4_004": {"battery": 11, "altitude": 30, "status": "returning", "payload_kg": 0.5},
}

# 1. Add a new key-value pair to the dictionary
fleet["PX4_005"] = {"battery": 95, "altitude": 0, "status": "standby", "payload_kg": 0}

# 2. .pop() removes the key and returns its value at the same time
removed_drone = fleet.pop("PX4_002")
print(f"Removed drone details: {removed_drone}")

# 3. Loop through keys and values. Print if status equals "active"
print("\nActive drones:")
for drone_id, info in fleet.items():
    if info["status"] == "active":
        print(f"  {drone_id}: {info['battery']}%")

# 4. Filter drones currently in the air (altitude > 0)
air_drones = {d_id: data for d_id, data in fleet.items() if data["altitude"] > 0}
# Find the drone key with the minimum battery value in the air_drones subset
lowest_air_batt = min(air_drones, key=lambda d: air_drones[d]["battery"])
print(f"\nLowest battery in air: {lowest_air_batt}")

# 5. Iterate and mutate the status for any drone with < 30 battery
for drone_id in fleet:
    if fleet[drone_id]["battery"] < 30:
        fleet[drone_id]["status"] = "critical_low_battery"

# 6. Print final dictionary
print(f"\nFinal fleet summary: {fleet}")







#Ans8






# Define three sets
planned = {"Z1", "Z2", "Z3", "Z5", "Z7"}
restricted = {"Z3", "Z5", "Z6", "Z8"}
cleared = {"Z1", "Z2", "Z3", "Z4", "Z5", "Z6", "Z7", "Z8"}

# 1. intersection() finds items existing in BOTH sets
print(f"Restricted planned zones: {planned.intersection(restricted)}")

# 2. difference() removes items found in the second set from the first set
print(f"Safe planned zones: {planned.difference(restricted)}")

# 3. symmetric_difference() finds items in either set, but NOT in both
print(f"Exclusive zones: {planned.symmetric_difference(restricted)}")

# 4. issubset() checks if every element in 'planned' exists inside 'cleared'
if planned.issubset(cleared):
    print("All planned zones are cleared.")
else:
    print("WARNING: Not all planned zones are cleared!")

# 5. Add and remove items from the mutable set
planned.add("Z9")
planned.remove("Z7")

# 6. union() combines sets, automatically eliminating duplicates
all_zones = planned.union(restricted, cleared)
print(f"Total unique zones across all sets: {len(all_zones)}")









#Ans9





# the drone's current condition in a dictionary
drone_state = {
    "battery": 18, 
    "altitude": 95, 
    "signal_strength": 40,
    "distance_from_home": 850, 
    "wind_speed": 38, 
    "obstacle_detected": True
}

# 1. Independent checks (using consecutive 'if' statements, not 'elif')
triggered = False
if drone_state["battery"] < 20:
    print("CRITICAL: RTH triggered - Low Battery")
    triggered = True
if drone_state["signal_strength"] < 30:
    print("WARNING: RTH triggered - Signal Lost")
    triggered = True
if drone_state["wind_speed"] > 35:
    print("WARNING: RTH triggered - High Wind")
    triggered = True
if drone_state["obstacle_detected"]:
    print("CAUTION: Obstacle detected - Rerouting")
    triggered = True
    
 # If no flag was set to True, all is well
if not triggered:
    print("All systems nominal")

# 2 & 3. Descent Loop
alt = drone_state["altitude"]
batt = drone_state["battery"]
print("\nInitiating descent:")

# Continue descending while altitude is greater than 0
while alt > 0:
    # Decrease altitude by 15 per step
    alt -= 15
    # Ensure altitude doesn't drop below 0
    if alt < 0:
        alt = 0
    # Drain battery by 1% per step
    batt -= 1
    # Print the current state
    print(f"Altitude: {alt}m, Battery: {batt}%")












#ans11








waypoints = [(0,0), (3,4), (6,8), (10,8), (10,0)]

def total_distance(waypoints, index=0):
    # 1. Base case: If we are at the last waypoint, distance to the next is 0
    if index >= len(waypoints) - 1:
        return 0
    
    # Extract coordinates for current and next point
    x1, y1 = waypoints[index]
    x2, y2 = waypoints[index + 1]
    
    # Calculate distance formula for the current leg
    dist = ((x2 - x1)**2 + (y2 - y1)**2)**0.5
    
    # 2. Recursively add this leg's distance to the distance of the remaining legs
    return dist + total_distance(waypoints, index + 1)

def find_longest_leg(waypoints, index=0, max_dist=0):
    # 1. Base case: Reached the end, return the highest distance recorded
    if index >= len(waypoints) - 1:
        return max_dist
    
    # Calculate distance for the current leg
    x1, y1 = waypoints[index]
    x2, y2 = waypoints[index + 1]
    dist = ((x2 - x1)**2 + (y2 - y1)**2)**0.5
    
    # Update max_dist if this current leg is longer than the previous record
    if dist > max_dist:
        max_dist = dist
        
    # 3. Recursive call, pushing the updated max_dist forward
    return find_longest_leg(waypoints, index + 1, max_dist)

# Print the outputs to verify
print("Total Distance:", total_distance(waypoints))
print("Longest Leg:", find_longest_leg(waypoints))









#ans13







# Take multiple inputs and convert them to integers
x = int(input("Enter starting x: "))
y = int(input("Enter starting y: "))
axis = input("Enter movement (horizontal or vertical): ").lower()
steps = int(input("Enter number of steps: "))

print("Output: ", end="")

# Loop for the exact number of steps requested
for step in range(steps):
    if axis == "horizontal":
        # Increment x by 1 for each horizontal step
        x += 1
    elif axis == "vertical":
        # Increment y by 1 for each vertical step
        y += 1
    # Print the coordinate update on every single move on the same line
    print(f"({x},{y}) ", end="")









#ans14







# Predefined credentials
true_id = "admin"
true_pass = "drone123"

# Accept input and convert to lowercase using .lower()
user_id = input("Enter ID: ").lower()
user_pass = input("Enter Password: ").lower()

# Compare against predefined strings
if user_id == true_id and user_pass == true_pass:
    print("Drone connected successfully")
else:
    print("Authentication failed")







#ans15








# Accept a string input
text = input("Enter a string: ")
print(f"You entered: {text}")

# Initialize a counter at zero
vowels = 0
# Check every character in the lowercase version of the string
for char in text.lower():
    # If the character exists in the string "aeiou", it's a vowel
    if char in "aeiou":
        vowels += 1
        
print(f"Number of vowels: {vowels}")






#ans16







# Take a single letter from the user
letter = input("Enter a lowercase letter: ")

# ord() gets the ASCII integer (e.g., 'a' is 97). 
# Subtracting 32 jumps to the uppercase ASCII equivalent (e.g., 'A' is 65).
upper_ascii = ord(letter) - 32
# chr() converts the new integer back into a character string
upper_letter = chr(upper_ascii)

print(f"Output: {upper_letter}")






#ans17
    










import cv2 as cv
import numpy as np

# Load the image
img = cv.imread(r"C:\Users\surya\OneDrive\Desktop\improve\landingpage.png")

# Convert the image to grayscale 
gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)

#  pixel above 200 becomes 255 
_, thresh = cv.threshold(gray, 200, 255, cv.THRESH_BINARY)

# Find contours
contours, _ = cv.findContours(thresh, cv.RETR_EXTERNAL, cv.CHAIN_APPROX_SIMPLE)

# Loop through the shapes
for cnt in contours:
    #  smooth out edges
    epsilon = 0.04 * cv.arcLength(cnt, True)
    approx = cv.approxPolyDP(cnt, epsilon, True)
    
    # If the  shape has exactly 4 sides our pad
    if len(approx) == 4:
        #  coordinates for the rectangle
        x, y, w, h = cv.boundingRect(approx)
        # Draw a green rectangle on the original 
        cv.rectangle(img, (x, y), (x+w, y+h), (0, 255, 0), 2)
        # Print action to terminal
        print("landing")
        break # We found the pad, no need to check other contours

# Save the final marked image to the disk
cv.imwrite("sahi.jpg", img)

