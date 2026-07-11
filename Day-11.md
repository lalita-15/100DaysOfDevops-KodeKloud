# 📝 Day 11 - XML String Replacement using `sed`

## 📑 Problem Statement

At xFusionCorp Industries, the Stratos Datacenter houses a jump host server that stores template XML files essential for the Nautilus application. Prior to their use, these files need to be populated with valid data. As part of regular maintenance, the system administration team utilizes various string and file manipulation commands to prepare these templates.

The task was to replace **all occurrences** of the string **`About`** with **`Marine`** in the XML file located at **`/root/nautilus.xml`** on the jump host server.

---

## 🎯 Objective

- Connect to the **Jump Host**.
- Locate the XML file **`/root/nautilus.xml`**.
- Replace every occurrence of **`About`** with **`Marine`**.
- Save the changes directly to the file.
- Verify that the replacement was successful.

---

## ⚙️ Solution
## Step 1: connect to App Server 2 

'''bash 
ssh thor@jump-host
'''

### Step 2:  Replace all occurrences

```bash
sed -i 's/About/Marine/g' /root/nautilus.xml
```

### Step 3: Verify the replacement

```bash
grep "About" /root/nautilus.xml
```

```bash
grep "Marine" /root/nautilus.xml
```

---

## Step 4: Verification

- No output from:

```bash
grep "About" /root/nautilus.xml
```

indicates that **all occurrences of `About` have been removed**.

- Output from:

```bash
grep "Marine" /root/nautilus.xml
```

confirms that the replacement was completed successfully.

---

## 📚 Key Concepts Learned

- Using the **`sed`** command for text manipulation.
- Editing files **in-place** with the **`-i`** option.
- Performing **global string replacement** using the **`g`** flag.
- Verifying file modifications using the **`grep`** command.
- Understanding the difference between replacing the first occurrence and replacing **all occurrences**.

---

##  Commands Used

```bash
sed -i 's/About/Marine/g' /root/nautilus.xml

grep "About" /root/nautilus.xml

grep "Marine" /root/nautilus.xml
```

---
