
#program 1 


import pandas as pd
from sklearn.preprocessing import LabelEncoder
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import MinMaxScaler

data = pd.read_csv('data1.csv')

print("Original Dataset")
print(data.head())

data.fillna(data.select_dtypes(include=['number']).mean(), inplace=True)

label_encoder = LabelEncoder()

for column in data.select_dtypes(include=['object', 'string']).columns:
    data[column] = label_encoder.fit_transform(data[column])

print("\nDataset after Encoding.")
print(data.head())

scaler = StandardScaler()
scaled_data = scaler.fit_transform(data)

scaled_df = pd.DataFrame(scaled_data, columns=data.columns)

print("\nStandardized Data:")
print(scaled_df.head())

normalizer = MinMaxScaler()
normalized_data = normalizer.fit_transform(data)

normalized_df = pd.DataFrame(normalized_data, columns=data.columns)

print("\nNormalized Data:")
print(normalized_df.head())




#program 2

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

data = pd.read_csv('Salary_Data.csv')

print("Statistical Summary:")
print(data.describe())

data.hist(figsize=(10, 8))
plt.suptitle("Feature Distribution")
plt.show()

correlation_matrix = data.corr(numeric_only=True)

print("\nCorrelation Matrix")
print(correlation_matrix)

plt.figure(figsize=(8, 6))
sns.heatmap(
    correlation_matrix,
    annot=True,
    cmap='coolwarm',
    linewidths=0.5
)

plt.title("Correlation Heatmap")
plt.show()

plt.figure(figsize=(10, 6))
sns.boxplot(data=data.select_dtypes(include=['int64', 'float64']))

plt.title("Boxplot for Outlier Detection")
plt.show()




#program 3

from sklearn.model_selection import train_test_split
from sklearn.model_selection import KFold
from sklearn.model_selection import cross_val_score
from sklearn.tree import DecisionTreeClassifier
from sklearn.datasets import load_iris

iris = load_iris()

X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

print("Training Set Size: ", len(X_train))
print("Test Set Size: ", len(X_test))

model = DecisionTreeClassifier(random_state=42)

kflod = KFold(n_splits=5, shuffle=True, random_state=42)

scores = cross_val_score(
    model, X_train, y_train, cv=kflod, scoring='accuracy'
)

print("\nAccuracy for each Fold:")

for i, score in enumerate(scores, start=1):
    print(f"Fold {i}: {score:.4f} ")

print("\nMean Accuracy:", scores.mean())
print("Standard Deviation:", scores.std())


#program 4A

import pandas as pd
import matplotlib.pyplot as plt
from pyparsing import lineEnd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

data = pd.DataFrame({
    'Experience': [1, 2, 3, 4, 5, 6, 7, 8],
    'Salary': [25000, 30000, 35000, 45000, 50000, 60000, 65000, 70000]
})

X = data[['Experience']]
y = data['Salary']

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print("MSE:", mse)
print("R2:", r2)

plt.scatter(X, y)
plt.plot(X, model.predict(X), linewidth=2)

plt.xlabel("Experience")
plt.ylabel("Salary")
plt.title("Simple Linear Regression")

plt.show()


#program 4B
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

data = pd.DataFrame({
    'Experience': [1, 2, 3, 4, 5, 6, 7, 8],
    'Education': [12, 12, 14, 14, 16, 16, 18, 18],
    'Salary': [25000, 30000, 35000, 45000, 50000, 60000, 65000, 70000]
})

X = data[['Experience', 'Education']]
y = data['Salary']

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print("MSE:", mse)
print("R2 Score:", r2)
print("Intercept:", model.intercept_)
print("Coefficient:", model.coef_)





#program 5

from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import confusion_matrix, accuracy_score

data = load_breast_cancer()

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size = 0.2, random_state = 42
)

model = LogisticRegression(max_iter=5000)

model.fit(X_train, y_train)

y_pred = model.predict(X_test)

cm = confusion_matrix(y_test, y_pred)

accuracy = accuracy_score(y_test, y_pred)

print("Confusion Matrix:", cm)
print("Accuracy:", accuracy)



#program 6


import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score

iris = load_iris()

x = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    x, y, test_size = 0.2, random_state = 42
)

k_values = [1, 3, 5, 7, 9]
accuracies = []

print("K_values \t Accuracy")

for k in k_values:
    knn = KNeighborsClassifier(n_neighbors=k)

    knn.fit(X_train, y_train)

    y_pred = knn.predict(X_test)

    accuracy = accuracy_score(y_test, y_pred)

    accuracies.append(accuracy)

    print(**f**"{k} \t\t {accuracy**:.4f**}")

plt.plot(k_values, accuracies, marker='o')

plt.xlabel("K_values")
plt.ylabel("Accuracy")
plt.title("KNN Accuracy for Different K Values")
plt.grid(True)

plt.show()







#program 7

from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report

iris = load_iris()

X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size = 0.2, random_state = 42
)

dt_model = DecisionTreeClassifier()

dt_model.fit(X_train, y_train)

dt_pred = dt_model.predict(X_test)

dt_accuracy = accuracy_score(y_test, dt_pred)

rf_model = RandomForestClassifier(
    n_estimators=100, random_state=42
)

rf_model.fit(X_train, y_train)

rf_pred = rf_model.predict(X_test)

rf_accuracy = accuracy_score(y_test, rf_pred)

print("Decision Tree Accuracy:", dt_accuracy)

print("Random Forest Accuracy:", rf_accuracy)

print("\n Decision Tree Classification Report:")

print(classification_report(y_test, dt_pred))

print("\n Random Forest Classification Report:")

print(classification_report(y_test, rf_pred))








#program 8

from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import precision_score
from sklearn.metrics import recall_score
from sklearn.metrics import f1_score
from sklearn.metrics import classification_report

data = load_breast_cancer()

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

model = GaussianNB()

model.fit(X_train, y_train)

y_pred = model.predict(X_test)

precision = precision_score(y_test, y_pred)

recall = recall_score(y_test, y_pred)

f1 = f1_score(y_test, y_pred)

print("Precision :", precision)
print("Recall    :", recall)
print("F1 Score  :", f1)

print("\nClassification Report")

print(classification_report(y_test, y_pred))






#program 9

from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score, classification_report

data = load_breast_cancer()

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

linear_svm = SVC(kernel='linear')

linear_svm.fit(X_train, y_train)

linear_pred = linear_svm.predict(X_test)

linear_accuracy = accuracy_score(y_test, linear_pred)

rbf_svm = SVC(kernel='rbf')

rbf_svm.fit(X_train, y_train)

rbf_pred = rbf_svm.predict(X_test)

rbf_accuracy = accuracy_score(y_test, rbf_pred)

print("Linear Kernel Accuracy :", linear_accuracy)

print("RBF Kernel Accuracy    :", rbf_accuracy)

print("\nLinear Kernel Classification Report")

print(classification_report(y_test, linear_pred))

print("\nRBF Kernel Classification Report")

print(classification_report(y_test, rbf_pred))






#program 10

import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.cluster import KMeans
from sklearn.cluster import AgglomerativeClustering
from scipy.cluster.hierarchy import dendrogram, linkage

iris = load_iris()

X = iris.data

wcss = []

for k in range(1, 11):
    kmeans = KMeans(
        n_clusters=k,
        init='k-means++',
        random_state=42,
        n_init=10
    )

    kmeans.fit(X)

    wcss.append(kmeans.inertia_)

plt.figure(figsize=(8, 5))

plt.plot(range(1, 11), wcss, marker='o')

plt.title("Elbow Method")
plt.xlabel("Number of Clusters (K)")
plt.ylabel("WCSS")

plt.show()

kmeans = KMeans(
    n_clusters=3,
    random_state=42,
    n_init=10
)

clusters = kmeans.fit_predict(X)

print("K-Means Cluster Labels:")
print(clusters)

linkage_matrix = linkage(X, method='ward')

plt.figure(figsize=(10, 5))

dendrogram(linkage_matrix)

plt.title("Dendrogram")
plt.xlabel("Data Points")
plt.ylabel("Euclidean Distance")

plt.show()

hc = AgglomerativeClustering(
    n_clusters=3,
    linkage='ward'
)

hc_clusters = hc.fit_predict(X)

print("\nHierarchical Clustering Labels:")
print(hc_clusters)








#program 11

from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

data = load_breast_cancer()

X = data.data
y = data.target

scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)

X_train, X_test, y_train, y_test = train_test_split(
    X_scaled, y, test_size=0.2, random_state=42
)

model_before = LogisticRegression(max_iter=5000)

model_before.fit(X_train, y_train)

y_pred_before = model_before.predict(X_test)

accuracy_before = accuracy_score(y_test, y_pred_before)

pca = PCA(n_components=10)

X_pca = pca.fit_transform(X_scaled)

X_train_pca, X_test_pca, y_train_pca, y_test_pca = train_test_split(
    X_pca, y, test_size=0.2, random_state=42
)

model_after = LogisticRegression(max_iter=5000)

model_after.fit(X_train_pca, y_train_pca)

y_pred_after = model_after.predict(X_test_pca)

accuracy_after = accuracy_score(y_test_pca, y_pred_after)

print("Accuracy Before PCA :", accuracy_before)

print("Accuracy After PCA  :", accuracy_after)

print("\nOriginal Features :", X.shape[1])

print("Reduced Features  :", X_pca.shape[1])

print("\nExplained Variance Ratio:")

print(pca.explained_variance_ratio_)









#program 12

from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.model_selection import GridSearchCV
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix

data = load_breast_cancer()

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', RandomForestClassifier(random_state=42))
])

param_grid = {
    'classifier__n_estimators': [50, 100, 150],
    'classifier__max_depth': [3, 5, 10],
    'classifier__min_samples_split': [2, 5]
}

grid_search = GridSearchCV(
    pipeline,
    param_grid,
    cv=5,
    scoring='accuracy',
    n_jobs=-1
)

grid_search.fit(X_train, y_train)

best_model = grid_search.best_estimator_

y_pred = best_model.predict(X_test)

accuracy = accuracy_score(y_test, y_pred)

cm = confusion_matrix(y_test, y_pred)

print("Best Parameters:")

print(grid_search.best_params_)

print("\nBest Cross Validation Score:")

print(grid_search.best_score_)

print("\nTest Accuracy:")

print(accuracy)

print("\nConfusion Matrix:")

print(cm)

print("\nClassification Report:")

print(classification_report(y_test, y_pred))
