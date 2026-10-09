# python-project1
📊 Workflow & Analysis Summary
Data Loading & Inspection

Reads Titanic-Dataset.csv into a Pandas DataFrame (df).

Checks basic dataset properties: shape (891 rows, 12 columns), column data types (dtypes), and non-null value counts (info()).

Data Health & Cleaning

Duplicates: Checked via df.duplicated().sum() (0 duplicates found).

Missing Values: Identifies missing values across columns:

Age: 177 missing values

Cabin: 687 missing values

Embarked: 2 missing values

Outlier Detection

Calculates the Interquartile Range (IQR) across integer columns (PassengerId, Survived, Pclass, SibSp, Parch) to identify numerical outliers using lower and upper bounds.

Data Aggregation & Grouping

Counts passenger records grouped by survival status (Survived), ticket IDs (Ticket), and ticket price (Fare).

EDA Dashboard & Visualizations
Creates a 2x2 grid of visualizations using seaborn and matplotlib:

Survival Rate by Passenger Class: Bar plot showing survival probability across classes (1st, 2nd, 3rd).

Age Distribution by Survival: KDE and step histogram comparing passenger ages relative to survival status.

Fare Distribution by Passenger Class: Box plot on a logarithmic scale highlighting fare spreads across passenger classes.

Passenger 
sns.set_theme(style="whitegrid")
fig, axes = plt.subplots(2, 2, figsize=(14, 10))
fig.suptitle('Titanic Dataset EDA Dashboard', fontsize=16, fontweight='bold')
sns.barplot(
    data=df, 
    x='Pclass', 
    y='Survived', 
    hue='Pclass', 
    legend=False, 
    ax=axes[0, 0], 
    palette='Blues_d', 
    errorbar=None
)
axes[0, 0].set_title('Survival Rate by Passenger Class')
axes[0, 0].set_ylabel('Survival Rate')
axes[0, 0].set_xlabel('Passenger Class (Pclass)')
sns.histplot(data=df, x='Age', hue='Survived', kde=True, ax=axes[0, 1], palette='Set1', element="step")
axes[0, 1].set_title('Age Distribution by Survival')
axes[0, 1].set_xlabel('Age')
sns.boxplot(
    data=df, 
    x='Pclass', 
    y='Fare', 
    hue='Pclass', 
    legend=False, 
    ax=axes[1, 0], 
    palette='Set2'
)
axes[1, 0].set_title('Fare Distribution by Passenger Class')
axes[1, 0].set_yscale('log') 
axes[1, 0].set_ylabel('Fare (Log Scale)')
sns.countplot(data=df, x='Sex', hue='Survived', ax=axes[1, 1], palette='pastel')
axes[1, 1].set_title('Passenger Count by Gender and Survival')
axes[1, 1].set_xlabel('Gender')
plt.tight_layout()
plt.show()
