# 1️⃣ Create an empty file
touch notes.txt

# 2️⃣ Write the first line (overwrite if file exists)
echo "Line 1" > notes.txt

# 3️⃣ Append the second line
echo "Line 2" >> notes.txt

# 4️⃣ Append the third line using tee (write and display at the same time)
echo "Line 3" | tee -a notes.txt

# 5️⃣ Read the full file
cat notes.txt

# 6️⃣ Read the first 2 lines
head -n 2 notes.txt

# 7️⃣ Read the last 2 lines
tail -n 2 notes.txt
