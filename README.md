
  

  import pandas as pd
mobiles = {
    "Samsung Galaxy": 25000,
    "iPhone 13": 65000,
    "OnePlus 11": 50000,
    "Redmi Note 12": 18000,
    "Realme Narzo": 15000
}

df = pd.DataFrame(list(mobiles.items()), columns=["Mobile Name", "Price"])

print("Mobile DataFrame:")
print(df)