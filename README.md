# house_price-car_price
{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "b2fbd133",
   "metadata": {},
   "source": [
    "# Car Price Prediction "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "6a68b8ca",
   "metadata": {},
   "source": [
    "Importing the Dependencies"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "bb861b90",
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns\n",
    "from sklearn.model_selection import train_test_split\n",
    "from sklearn.linear_model import LinearRegression\n",
    "from sklearn.linear_model import Lasso\n",
    "from sklearn import metrics"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "6a70031b",
   "metadata": {},
   "outputs": [],
   "source": [
    "# loading the data from csv file to pandas dataframe\n",
    "car_dataset = pd.read_csv('D:\\panda/car data.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "ae304c25",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Car_Name</th>\n",
       "      <th>Year</th>\n",
       "      <th>Selling_Price</th>\n",
       "      <th>Present_Price</th>\n",
       "      <th>Kms_Driven</th>\n",
       "      <th>Fuel_Type</th>\n",
       "      <th>Seller_Type</th>\n",
       "      <th>Transmission</th>\n",
       "      <th>Owner</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>ritz</td>\n",
       "      <td>2014</td>\n",
       "      <td>3.35</td>\n",
       "      <td>5.59</td>\n",
       "      <td>27000</td>\n",
       "      <td>Petrol</td>\n",
       "      <td>Dealer</td>\n",
       "      <td>Manual</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>sx4</td>\n",
       "      <td>2013</td>\n",
       "      <td>4.75</td>\n",
       "      <td>9.54</td>\n",
       "      <td>43000</td>\n",
       "      <td>Diesel</td>\n",
       "      <td>Dealer</td>\n",
       "      <td>Manual</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>ciaz</td>\n",
       "      <td>2017</td>\n",
       "      <td>7.25</td>\n",
       "      <td>9.85</td>\n",
       "      <td>6900</td>\n",
       "      <td>Petrol</td>\n",
       "      <td>Dealer</td>\n",
       "      <td>Manual</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>wagon r</td>\n",
       "      <td>2011</td>\n",
       "      <td>2.85</td>\n",
       "      <td>4.15</td>\n",
       "      <td>5200</td>\n",
       "      <td>Petrol</td>\n",
       "      <td>Dealer</td>\n",
       "      <td>Manual</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>swift</td>\n",
       "      <td>2014</td>\n",
       "      <td>4.60</td>\n",
       "      <td>6.87</td>\n",
       "      <td>42450</td>\n",
       "      <td>Diesel</td>\n",
       "      <td>Dealer</td>\n",
       "      <td>Manual</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  Car_Name  Year  Selling_Price  Present_Price  Kms_Driven Fuel_Type  \\\n",
       "0     ritz  2014           3.35           5.59       27000    Petrol   \n",
       "1      sx4  2013           4.75           9.54       43000    Diesel   \n",
       "2     ciaz  2017           7.25           9.85        6900    Petrol   \n",
       "3  wagon r  2011           2.85           4.15        5200    Petrol   \n",
       "4    swift  2014           4.60           6.87       42450    Diesel   \n",
       "\n",
       "  Seller_Type Transmission  Owner  \n",
       "0      Dealer       Manual      0  \n",
       "1      Dealer       Manual      0  \n",
       "2      Dealer       Manual      0  \n",
       "3      Dealer       Manual      0  \n",
       "4      Dealer       Manual      0  "
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# inspecting the first 5 rows of the dataframe\n",
    "car_dataset.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "a9a053f9",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(301, 9)"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# checking the number of rows and columns\n",
    "car_dataset.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "a2e17858",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 301 entries, 0 to 300\n",
      "Data columns (total 9 columns):\n",
      " #   Column         Non-Null Count  Dtype  \n",
      "---  ------         --------------  -----  \n",
      " 0   Car_Name       301 non-null    object \n",
      " 1   Year           301 non-null    int64  \n",
      " 2   Selling_Price  301 non-null    float64\n",
      " 3   Present_Price  301 non-null    float64\n",
      " 4   Kms_Driven     301 non-null    int64  \n",
      " 5   Fuel_Type      301 non-null    object \n",
      " 6   Seller_Type    301 non-null    object \n",
      " 7   Transmission   301 non-null    object \n",
      " 8   Owner          301 non-null    int64  \n",
      "dtypes: float64(2), int64(3), object(4)\n",
      "memory usage: 21.3+ KB\n"
     ]
    }
   ],
   "source": [
    "# getting some information about the dataset\n",
    "car_dataset.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "58fee2cb",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Car_Name         0\n",
       "Year             0\n",
       "Selling_Price    0\n",
       "Present_Price    0\n",
       "Kms_Driven       0\n",
       "Fuel_Type        0\n",
       "Seller_Type      0\n",
       "Transmission     0\n",
       "Owner            0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# checking the number of missing values\n",
    "car_dataset.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "5b1bd837",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Petrol    239\n",
      "Diesel     60\n",
      "CNG         2\n",
      "Name: Fuel_Type, dtype: int64\n",
      "Dealer        195\n",
      "Individual    106\n",
      "Name: Seller_Type, dtype: int64\n",
      "Manual       261\n",
      "Automatic     40\n",
      "Name: Transmission, dtype: int64\n"
     ]
    }
   ],
   "source": [
    "# checking the distribution of categorical data\n",
    "print(car_dataset.Fuel_Type.value_counts())\n",
    "print(car_dataset.Seller_Type.value_counts())\n",
    "print(car_dataset.Transmission.value_counts())"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "6e5ae9c9",
   "metadata": {},
   "source": [
    "# Encoding the Categorical Data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "54e43929",
   "metadata": {},
   "outputs": [],
   "source": [
    "# encoding \"Fuel_Type\" Column\n",
    "car_dataset.replace({'Fuel_Type':{'Petrol':0,'Diesel':1,'CNG':2}},inplace=True)\n",
    "\n",
    "# encoding \"Seller_Type\" Column\n",
    "car_dataset.replace({'Seller_Type':{'Dealer':0,'Individual':1}},inplace=True)\n",
    "\n",
    "# encoding \"Transmission\" Column\n",
    "car_dataset.replace({'Transmission':{'Manual':0,'Automatic':1}},inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "b8965a75",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Car_Name</th>\n",
       "      <th>Year</th>\n",
       "      <th>Selling_Price</th>\n",
       "      <th>Present_Price</th>\n",
       "      <th>Kms_Driven</th>\n",
       "      <th>Fuel_Type</th>\n",
       "      <th>Seller_Type</th>\n",
       "      <th>Transmission</th>\n",
       "      <th>Owner</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>ritz</td>\n",
       "      <td>2014</td>\n",
       "      <td>3.35</td>\n",
       "      <td>5.59</td>\n",
       "      <td>27000</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>sx4</td>\n",
       "      <td>2013</td>\n",
       "      <td>4.75</td>\n",
       "      <td>9.54</td>\n",
       "      <td>43000</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>ciaz</td>\n",
       "      <td>2017</td>\n",
       "      <td>7.25</td>\n",
       "      <td>9.85</td>\n",
       "      <td>6900</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>wagon r</td>\n",
       "      <td>2011</td>\n",
       "      <td>2.85</td>\n",
       "      <td>4.15</td>\n",
       "      <td>5200</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>swift</td>\n",
       "      <td>2014</td>\n",
       "      <td>4.60</td>\n",
       "      <td>6.87</td>\n",
       "      <td>42450</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  Car_Name  Year  Selling_Price  Present_Price  Kms_Driven  Fuel_Type  \\\n",
       "0     ritz  2014           3.35           5.59       27000          0   \n",
       "1      sx4  2013           4.75           9.54       43000          1   \n",
       "2     ciaz  2017           7.25           9.85        6900          0   \n",
       "3  wagon r  2011           2.85           4.15        5200          0   \n",
       "4    swift  2014           4.60           6.87       42450          1   \n",
       "\n",
       "   Seller_Type  Transmission  Owner  \n",
       "0            0             0      0  \n",
       "1            0             0      0  \n",
       "2            0             0      0  \n",
       "3            0             0      0  \n",
       "4            0             0      0  "
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "car_dataset.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "14de2b64",
   "metadata": {},
   "source": [
    "# Splitting the data and Target"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "3f16fa06",
   "metadata": {},
   "outputs": [],
   "source": [
    "X = car_dataset.drop(['Car_Name','Selling_Price'],axis=1)\n",
    "Y = car_dataset['Selling_Price']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "56040af3",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "     Year  Present_Price  Kms_Driven  Fuel_Type  Seller_Type  Transmission  \\\n",
      "0    2014           5.59       27000          0            0             0   \n",
      "1    2013           9.54       43000          1            0             0   \n",
      "2    2017           9.85        6900          0            0             0   \n",
      "3    2011           4.15        5200          0            0             0   \n",
      "4    2014           6.87       42450          1            0             0   \n",
      "..    ...            ...         ...        ...          ...           ...   \n",
      "296  2016          11.60       33988          1            0             0   \n",
      "297  2015           5.90       60000          0            0             0   \n",
      "298  2009          11.00       87934          0            0             0   \n",
      "299  2017          12.50        9000          1            0             0   \n",
      "300  2016           5.90        5464          0            0             0   \n",
      "\n",
      "     Owner  \n",
      "0        0  \n",
      "1        0  \n",
      "2        0  \n",
      "3        0  \n",
      "4        0  \n",
      "..     ...  \n",
      "296      0  \n",
      "297      0  \n",
      "298      0  \n",
      "299      0  \n",
      "300      0  \n",
      "\n",
      "[301 rows x 7 columns]\n"
     ]
    }
   ],
   "source": [
    "print(X)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "23f8ac54",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "0       3.35\n",
      "1       4.75\n",
      "2       7.25\n",
      "3       2.85\n",
      "4       4.60\n",
      "       ...  \n",
      "296     9.50\n",
      "297     4.00\n",
      "298     3.35\n",
      "299    11.50\n",
      "300     5.30\n",
      "Name: Selling_Price, Length: 301, dtype: float64\n"
     ]
    }
   ],
   "source": [
    "print(Y)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4d7770f8",
   "metadata": {},
   "source": [
    "# Splitting Training and Test data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "66f7b831",
   "metadata": {},
   "outputs": [],
   "source": [
    "X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size = 0.1, random_state=2)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a5d74b0b",
   "metadata": {},
   "source": [
    "# Model Training"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "fb5a2602",
   "metadata": {},
   "source": [
    "1. Linear Regression"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "5dd32495",
   "metadata": {},
   "outputs": [],
   "source": [
    "# loading the linear regression model\n",
    "lin_reg_model = LinearRegression()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "0a1551fd",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "LinearRegression()"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "lin_reg_model.fit(X_train,Y_train)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "73b7dc70",
   "metadata": {},
   "source": [
    "# Model Evaluation"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "02e17f75",
   "metadata": {},
   "outputs": [],
   "source": [
    "# prediction on Training data\n",
    "training_data_prediction = lin_reg_model.predict(X_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "a6e19afa",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "R squared Error :  0.8799451660493701\n"
     ]
    }
   ],
   "source": [
    "# R squared Error\n",
    "error_score = metrics.r2_score(Y_train, training_data_prediction)\n",
    "print(\"R squared Error : \", error_score)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "117a80b3",
   "metadata": {},
   "source": [
    "# Visualize the actual prices and Predicted prices"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "1f68d7db",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.scatter(Y_train, training_data_prediction)\n",
    "plt.xlabel(\"Actual Price\")\n",
    "plt.ylabel(\"Predicted Price\")\n",
    "plt.title(\" Actual Prices vs Predicted Prices\")\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "id": "3bbbde57",
   "metadata": {},
   "outputs": [],
   "source": [
    "# prediction on Training data\n",
    "test_data_prediction = lin_reg_model.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "id": "a7420a38",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "R squared Error :  0.836576671502687\n"
     ]
    }
   ],
   "source": [
    "# R squared Error\n",
    "error_score = metrics.r2_score(Y_test, test_data_prediction)\n",
    "print(\"R squared Error : \", error_score)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "id": "a20966b9",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.scatter(Y_test, test_data_prediction)\n",
    "plt.xlabel(\"Actual Price\")\n",
    "plt.ylabel(\"Predicted Price\")\n",
    "plt.title(\" Actual Prices vs Predicted Prices\")\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "0c461a49",
   "metadata": {},
   "source": [
    "2. Lasso Regression"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "id": "62af366d",
   "metadata": {},
   "outputs": [],
   "source": [
    "# loading the linear regression model\n",
    "lass_reg_model = Lasso()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "id": "23fe1d81",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Lasso()"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "lass_reg_model.fit(X_train,Y_train)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9914b95b",
   "metadata": {},
   "source": [
    "# Model Evaluation"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "d7414cdd",
   "metadata": {},
   "outputs": [],
   "source": [
    "# prediction on Training data\n",
    "training_data_prediction = lass_reg_model.predict(X_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "id": "a8080613",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "R squared Error :  0.8427856123435794\n"
     ]
    }
   ],
   "source": [
    "# R squared Error\n",
    "error_score = metrics.r2_score(Y_train, training_data_prediction)\n",
    "print(\"R squared Error : \", error_score)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "601d07f6",
   "metadata": {},
   "source": [
    "# Visualize the actual prices and Predicted prices"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "id": "adabf4b6",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.scatter(Y_train, training_data_prediction)\n",
    "plt.xlabel(\"Actual Price\")\n",
    "plt.ylabel(\"Predicted Price\")\n",
    "plt.title(\" Actual Prices vs Predicted Prices\")\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "id": "aefcdabe",
   "metadata": {},
   "outputs": [],
   "source": [
    "# prediction on Training data\n",
    "test_data_prediction = lass_reg_model.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "id": "138bbf45",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "R squared Error :  0.8709167941173195\n"
     ]
    }
   ],
   "source": [
    "# R squared Error\n",
    "error_score = metrics.r2_score(Y_test, test_data_prediction)\n",
    "print(\"R squared Error : \", error_score)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "id": "ff59e662",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.scatter(Y_test, test_data_prediction)\n",
    "plt.xlabel(\"Actual Price\")\n",
    "plt.ylabel(\"Predicted Price\")\n",
    "plt.title(\" Actual Prices vs Predicted Prices\")\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "c12d7bcb",
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.7"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
