# PySpark-ML-for-Fifa

# Problem
This dataset contains Soccer player statistics for 2015-2022. In this project we firstly perform data engineering on 110 columns. Then, we build machine learning models that predict the overall value for each player based on their skillsets.

# Constraints
<li>unique_id: This column could be used as a primary key if it offers unique values for each record.</li>
<li>sofifa_id and year: A combination of these two columns should be unique because a player can only have one set of stats for a particular year.</li>
<li>age: Must be positive and within a realistic range for professional soccer players.</li>
<li>height_cm: Positive value constraint.</li>
<li>weight_kg: Positive value constraint.</li>
<li>overall, potential, and all other rating columns: These ratings typically fall within the range 0 to 100.</li>
<li>Columns like sofifa_id, short_name, long_name, age, dob, and year should always have values. This is because these are crucial pieces of information for each player record.</li>
<li>preferred_foot: Could be limited to known values: 'Left' or 'Right'.</li>
<li>work_rate: Might be limited to specific combinations, e.g., 'Medium/Low', 'High/Medium', etc.</li>
<li>player_positions, club_position, and nation_position: These can be enumerated to a list of soccer positions.</li>

# Description of Features
<li>sofifa_id: Unique ID for each player.</li>
<li>player_url: URL for the player's profile on Sofifa.</li>
<li>player_face_url: URL for the player's image.</li>
<li>club_logo_url: URL for the player's club logo.</li>
<li>club_flag_url: URL for the player's club flag.</li>
<li>nation_logo_url: URL for the player's national team logo.</li>
<li>nation_flag_url: URL for the player's national flag.</li>
<li>short_name: Short version of the player's name.</li>
<li>long_name: Full name of the player.</li>
<li>player_positions: The positions the player can play.</li>
<li>overall: Player's overall rating.</li>
<li>potential: Player's potential rating (future capability).</li>
<li>value_eur: Player's estimated market value in Euros.</li>
<li>wage_eur: Player's weekly wage in Euros.</li>
<li>age: Player's age.</li>
<li>Columns like pace, shooting, passing, etc., represent specific skills and abilities of players.</li>
<li>Metrics like attacking_crossing, movement_acceleration, defending_marking_awareness, and many more that give more granular details about the player's attributes in various facets of the game.</li>
<li>Columns like ls, st, cb, gk, etc., represent the player's rating for specific positions on the soccer field. These ratings can provide insights into how proficient a player is in various positions.</li>
<li>dob: Date of birth of the player.</li>
<li>club_name: Name of the club the player belongs to.</li>
<li>league_name: Name of the league in which the player's club competes.</li>
<li>club_position: Player's position in the club.</li>
<li>club_loaned_from: Club from which the player is loaned (if applicable).</li>
<li>club_joined: Date when the player joined the current club.</li>
<li>nationality_name: Player's nationality.</li>
<li>nation_position: Player's position in the national team.</li>
<li>preferred_foot: Player's dominant foot (left/right).</li>
<li>work_rate: Player's work rate.</li>
<li>real_face: Indicates if the player's image is a real photo or a graphic representation.</li>
<li>player_tags & player_traits: Specific tags and traits associated with the player.</li>
<li>Columns like lw, lf, cf, etc., are likely related to the player's proficiency or ratings in certain advanced positions.</li>

# Model Selection: Spark
## Linear Regression
1. Reason for selection: We use Linear Regression because it is a simple way to start trying with. Initially, we simply expect there is a linear relationship between features and target variable.
2. Parameter Tuning
   - We use regularization to prevent the overfitting. We select 0.1 as a moderate regularization.
   - We use ElasticNet Mixing to balance between L1 and L2 regularization. L1 can lead to sparsity whereas L2 can lead to the coefficients regularized evenly.
   - We use iterations to restrict the number of iterations we'll perform. It can avoid the complexity of training.

## Decision Tree
1. Reason for selection: Comparing to linear regression, Decision Tree can capture non-linear relationships between features and target variables.
2. Parameter Tuning
   - We use MaxDepth to control the complexity of the model. And we try various range to check how it performs.
   - We use MaxBins to deal with continuous features. With more bins, we can have more detailed distinctions between values, but may lead to overfitting.
  
# Model Selection: PyTorch
## Shallow MLP
1. Reason: We choose this for the simplicity and speed. Also, if the relationship int he data is not very complex, shallow MLP can prevent overfitting.

## Deep MLP
1. Reason: We choose this to further model the relationship in the data, where deeper network can capture more complex pattern in the data.

## Parameters for these MLPs
1. Learning rate: This controls how fast the network updates its weight. If the learning rate is too high, the network may overshoot the optimal solution. If it's too low, training may be too slow or get stuck in a local minimum.
2. Activation function: We just use a standard choise ReLU, which can help with the vanishing gradient problem.
3. Loss function:We select it because we are dealing with a regression problem.
4. Optimizer: We use Adam, a standard choice which can handle sparse gradients on noisy problems.
