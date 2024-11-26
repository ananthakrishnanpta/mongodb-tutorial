# Setting Up MongoDB Atlas

Follow these steps to set up a free MongoDB Atlas cluster:

### Step 1: Create an Atlas Account
1. Visit [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) and sign up.
2. Log in and create a project.

### Step 2: Configure Your Cluster
1. Create a new cluster using the free-tier option.
2. Choose a cloud provider and region.

### Step 3: Database Access
1. Go to **Database Access**.
2. Add a new user with `readWriteAnyDatabase` permissions.

### Step 4: Network Access
1. Go to **Network Access**.
2. Whitelist your IP (`0.0.0.0/0` for open access during testing).

### Step 5: Connection String
1. Copy the connection string (e.g., `mongodb+srv://<username>:<password>@cluster0.mongodb.net/test`).

---

[Next: Configuring a Persistent Connection](04-configuring-persistent-connection.md)
