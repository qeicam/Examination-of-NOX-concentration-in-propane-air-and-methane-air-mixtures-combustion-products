import cantera as ct
import matplotlib.pyplot as plt

# Approach 1 
###
n = 120  # number of steps
k = 0.01  # step length
equivalence_ratios = [0 + (i * k) for i in range(n)]  # vector containing equivalence ratios
###
A1_no_molar_fraction = []
A1_no2_molar_fraction = []
A1_temp_in = 2100  # initial temperature in Kelvins
A1_pressure_in = 6e6  # initial pressure in Pascals
for equivalence_ratio in equivalence_ratios:
    A1 = ct.Solution('gri30.yaml')
    A1.TPX = A1_temp_in, A1_pressure_in, f'CH4:{equivalence_ratio}, O2:2, N2:7.52'

    # define simulation duration
    A1_reaction_time = 1  # Reaction extent in seconds

    # perform the combustion simulation in constant pressure for Brayton cycle
    A1_reactor = ct.IdealGasConstPressureReactor(A1)
    A1_sim = ct.ReactorNet([A1_reactor])
    A1_sim.advance(A1_reaction_time)

    # fill vectors containing info about molar fractions of nox
    A1_no_molar_fraction.append(A1.X[35])
    A1_no2_molar_fraction.append(A1.X[36])

A1_nox_molar_fraction = []
for i in range(len(A1_no_molar_fraction)):
    A1_nox_molar_fraction.append(A1_no_molar_fraction[i] + A1_no2_molar_fraction[i])
A1_nox_molar_concentration = []
for i in range(len(A1_no_molar_fraction)):
    A1_nox_molar_concentration.append(A1_nox_molar_fraction[i] * 100)
fig1 = plt.figure(1)
plt.plot(equivalence_ratios, A1_nox_molar_concentration)
plt.xlabel('Equivalence ratio, φ')
plt.ylabel('Molar concentration of NOx, [%]')
plt.title('Relation between molar concentration of NOx and equivalence ratio for methane at T = 2100K, p = 6 MPa')
plt.grid(True)

# Approach 2
###
n = 120  
k = 0.01 
equivalence_ratios = [0 + (i * k) for i in range(n)]  
###
A2_no_molar_fraction = []
A2_no2_molar_fraction = []
A2_temp_in = 2400 # initial temperature in Kelvins
A2_pressure_in = 6e6  # initial pressure in Pascals
for equivalence_ratio in equivalence_ratios:
    A2 = ct.Solution('gri30.yaml')
    A2.TPX = A2_temp_in, A2_pressure_in, f'CH4:{equivalence_ratio}, O2:2, N2:7.52'

    # define simulation duration
    A2_reaction_time = 1  # Reaction duration in seconds

    # perform the combustion simulation in constant pressure
    A2_reactor = ct.IdealGasConstPressureReactor(A2)
    A2_sim = ct.ReactorNet([A2_reactor])
    A2_sim.advance(A2_reaction_time)

    # fill vectors containing info about molar fractions of nox
    A2_no_molar_fraction.append(A2.X[35])
    A2_no2_molar_fraction.append(A2.X[36])

A2_nox_molar_fraction = []
for i in range(len(A2_no_molar_fraction)):
    A2_nox_molar_fraction.append(A2_no_molar_fraction[i] + A2_no2_molar_fraction[i])
A2_nox_molar_concentration = []
for i in range(len(A2_no_molar_fraction)):
    A2_nox_molar_concentration.append(A2_nox_molar_fraction[i] * 100)
fig2 = plt.figure(2)
plt.plot(equivalence_ratios, A2_nox_molar_concentration)
plt.xlabel('Equivalence ratio, φ')
plt.ylabel('Molar concentration of NOx, [%]')
plt.title('Relation between molar concentration of NOx and equivalence ratio methane at T = 2400K, p = 6 MPa')
plt.grid(True)

# Approach 3 
###
n = 120 
k = 0.01
equivalence_ratios = [0 + (i * k) for i in range(n)] 
###
A3_no_molar_fraction = []
A3_no2_molar_fraction = []
A3_temp_in = 2700  # initial temperature in Kelvins
A3_pressure_in = 6e6  # initial pressure in Pascals
for equivalence_ratio in equivalence_ratios:
    A3 = ct.Solution('gri30.yaml')
    A3.TPX = A3_temp_in, A3_pressure_in, f'CH4:{equivalence_ratio}, O2:2, N2:7.52'

    # define simulation time
    A3_reaction_time = 1  # Reaction extent in seconds

    # perform the combustion simulation in constant volume
    A3_reactor = ct.IdealGasConstPressureReactor(A3)
    A3_sim = ct.ReactorNet([A3_reactor])
    A3_sim.advance(A3_reaction_time)

    # fill vectors containing info about molar fractions of nox
    A3_no_molar_fraction.append(A3.X[35])
    A3_no2_molar_fraction.append(A3.X[36])

A3_nox_molar_fraction = []
for i in range(len(A3_no_molar_fraction)):
    A3_nox_molar_fraction.append(A3_no_molar_fraction[i] + A3_no2_molar_fraction[i])
A3_nox_molar_concentration = []
for i in range(len(A3_no_molar_fraction)):
    A3_nox_molar_concentration.append(A3_nox_molar_fraction[i] * 100)
fig3 = plt.figure(3)
plt.plot(equivalence_ratios, A3_nox_molar_concentration)
plt.xlabel('Equivalence ratio, φ')
plt.ylabel('Molar concentration of NOx, [%]')
plt.title('Relation between molar concentration of NOx and equivalence ratio for methane at T = 2700K, p = 6 MPa')
plt.grid(True)

# Approach 4 
###
n = 240  
k = 0.005
equivalence_ratios = [0 + (i * k) for i in range(n)]  
###
A4_no_molar_fraction = []
A4_no2_molar_fraction = []
A4_temp_in = 2100  # initial temperature in Kelvins
A4_pressure_in = 6e6  # initial pressure in Pascals
for equivalence_ratio in equivalence_ratios:
    A4 = ct.Solution('gri30.yaml')
    A4.TPX = A4_temp_in, A4_pressure_in, f'C3H8:{equivalence_ratio}, O2:5, N2:18.8'

    # define simulation time
    A4_reaction_time = 1  # Reaction extent in seconds

    # perform the combustion simulation in constant volume
    A4_reactor = ct.IdealGasConstPressureReactor(A4)
    A4_sim = ct.ReactorNet([A4_reactor])
    A4_sim.advance(A4_reaction_time)

    # fill vectors containing info about molar fractions of nox
    A4_no_molar_fraction.append(A4.X[35])
    A4_no2_molar_fraction.append(A4.X[36])

A4_nox_molar_fraction = []
for i in range(len(A4_no_molar_fraction)):
    A4_nox_molar_fraction.append(A4_no_molar_fraction[i] + A4_no2_molar_fraction[i])
A4_nox_molar_concentration = []
for i in range(len(A4_no_molar_fraction)):
    A4_nox_molar_concentration.append(A4_nox_molar_fraction[i] * 100)
fig4 = plt.figure(4)
plt.plot(equivalence_ratios, A4_nox_molar_concentration)
plt.xlabel('Equivalence ratio, φ')
plt.ylabel('Molar concentration of NOx, [%]')
plt.title('Relation between molar concentration of NOx and equivalence ratio for propane at T = 2100K, p = 6 MPa')
plt.grid(True)

# Approach 5
###
n = 240  
k = 0.005  
equivalence_ratios = [0 + (i * k) for i in range(n)]  
###
A5_no_molar_fraction = []
A5_no2_molar_fraction = []
A5_temp_in = 2400  # initial temperature in Kelvins
A5_pressure_in = 6e6  # initial pressure in Pascals
for equivalence_ratio in equivalence_ratios:
    A5 = ct.Solution('gri30.yaml')
    A5.TPX = A5_temp_in, A5_pressure_in, f'C3H8:{equivalence_ratio}, O2:5, N2:18.8'

    # define simulation time
    A5_reaction_time = 1  # Reaction extent in seconds

    # perform the combustion simulation in constant volume
    A5_reactor = ct.IdealGasConstPressureReactor(A5)
    A5_sim = ct.ReactorNet([A5_reactor])
    A5_sim.advance(A5_reaction_time)

    # fill vectors containing info about molar fractions of nox
    A5_no_molar_fraction.append(A5.X[35])
    A5_no2_molar_fraction.append(A5.X[36])

A5_nox_molar_fraction = []
for i in range(len(A5_no_molar_fraction)):
    A5_nox_molar_fraction.append(A5_no_molar_fraction[i] + A5_no2_molar_fraction[i])
A5_nox_molar_concentration = []
for i in range(len(A5_no_molar_fraction)):
    A5_nox_molar_concentration.append(A5_nox_molar_fraction[i] * 100)
fig5 = plt.figure(5)
plt.plot(equivalence_ratios, A5_nox_molar_concentration)
plt.xlabel('Equivalence ratio, φ')
plt.ylabel('Molar concentration of NOx, [%]')
plt.title('Relation between molar concentration of NOx and equivalence ratio for propane at T = 2400K, p = 6 MPa')
plt.grid(True)

# Approach 6
###
n = 240 
k = 0.005  
equivalence_ratios = [0 + (i * k) for i in range(n)]  
###
A6_no_molar_fraction = []
A6_no2_molar_fraction = []
A6_temp_in = 2700  # initial temperature in Kelvins
A6_pressure_in = 6e6  # initial pressure in Pascals
for equivalence_ratio in equivalence_ratios:
    A6 = ct.Solution('gri30.yaml')
    A6.TPX = A6_temp_in, A6_pressure_in, f'C3H8:{equivalence_ratio}, O2:5, N2:18.8'

    # define simulation time
    A6_reaction_time = 1  # Reaction extent in seconds

    # perform the combustion simulation in constant volume
    A6_reactor = ct.IdealGasConstPressureReactor(A6)
    A6_sim = ct.ReactorNet([A6_reactor])
    A6_sim.advance(A6_reaction_time)

    # fill vectors containing info about molar fractions of nox
    A6_no_molar_fraction.append(A6.X[35])
    A6_no2_molar_fraction.append(A6.X[36])

A6_nox_molar_fraction = []
for i in range(len(A6_no_molar_fraction)):
    A6_nox_molar_fraction.append(A6_no_molar_fraction[i] + A6_no2_molar_fraction[i])
A6_nox_molar_concentration = []
for i in range(len(A6_no_molar_fraction)):
    A6_nox_molar_concentration.append(A6_nox_molar_fraction[i] * 100)
fig6 = plt.figure(6)
plt.plot(equivalence_ratios, A6_nox_molar_concentration)
plt.xlabel('Equivalence ratio, φ')
plt.ylabel('Molar concentration of NOx, [%]')
plt.title('Relation between molar concentration of NOx and equivalence ratio for propane at T = 2700K, p = 6 MPa')
plt.grid(True)
plt.show()