# username.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>UDS MANUAL GPA & CGPA Calculator</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      padding: 30px;
      background: #e0f7e9; /* Light Green */
      color: #003300;
      position: relative;
      min-height: 100vh;
    }

    h1, h2 {
      color: #006400; /* Deep Green */
    }

    label, p {
      font-size: 16px;
    }

    select, input, button {
      padding: 10px;
      margin: 5px;
      border-radius: 5px;
      border: 1px solid #ccc;
      font-size: 14px;
    }

    button {
      background-color: #006400;
      color: white;
      border: none;
    }

    button:hover {
      background-color: #004d00;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-bottom: 20px;
      background: #ffffff;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
    }

    th {
      background-color: #006400;
      color: white;
      padding: 10px;
    }

    td {
      padding: 30px;
      text-align: center;
    }

    input[type="text"], input[type="number"], select {
      width: 90%;
    }

    .results {
      background: #d4f5e4;
      border-left: 6px solid #006400;
      padding: 20px;
      margin-top: 20px;
      border-radius: 5px;
    }

    .hidden {
      display: none;
    }

    .highlight {
      color: #004d00;
      font-weight: bold;
    }

    #calcMode {
      margin-bottom: 20px;
    }

    /* Header and Help Button Styles */
    .header-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }

    #helpBtn {
      background-color: #006400;
      color: white;
      padding: 10px 15px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    #helpBtn:hover {
      background-color: #004d00;
    }

    /* Footer Styles */
    footer {
      text-align: center;
      margin-top: 30px;
      padding: 10px;
      color: #006400;
      font-size: 14px;
    }

    /* Help Modal Styles */
    .modal {
      display: none;
      position: fixed;
      z-index: 1;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.4);
    }

    .modal-content {
      background-color: #f8fff8;
      margin: 10% auto;
      padding: 20px;
      border: 1px solid #006400;
      width: 60%;
      border-radius: 5px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    }

    .close {
      color: #006400;
      float: right;
      font-size: 28px;
      font-weight: bold;
      cursor: pointer;
    }

    .close:hover {
      color: #004d00;
    }
  </style>
</head>
<body>

  <div class="header-container">
    <h1>WELCOME TO UDS MANUAL GPA & CGPA Calculator</h1>
    <button id="helpBtn" onclick="openHelp()">Help</button>
  </div>

  <label for="calcMode"><strong>Select Calculation Mode:</strong></label>
  <select id="calcMode" onchange="toggleMode()">
    <option value="gpa">GPA (Current Trimester Only)</option>
    <option value="cgpa">CGPA (Cumulative)</option>
  </select>

  <!-- GPA Section -->
  <div id="gpaSection">
    <h2>Enter Courses for Current Trimester</h2>
    <table id="courseTable">
      <thead>
        <tr>
          <th>Course Name</th>
          <th>Credit Hours</th>
          <th>Score (0-100)</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><input type="text" placeholder="e.g. MATH101" /></td>
          <td><input type="number" min="1" max="6" value="3" /></td>
          <td><input type="number" min="0" max="100" placeholder="Enter score" /></td>
          <td><button onclick="removeRow(this)">Remove</button></td>
        </tr>
      </tbody>
    </table>
    <button onclick="addRow()">Add Course</button>
    <button onclick="calculateGPA()">Calculate GPA</button>
  </div>

  <!-- CGPA Section -->
  <div id="cgpaSection" class="hidden">
    <h2>Enter Previous Trimester GPAs</h2>
    <table id="cgpaTable">
      <thead>
        <tr>
          <th>Trimester</th>
          <th>GPA</th>
          <th>Credit Hours</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><input type="text" placeholder="e.g. L100 T1" /></td>
          <td><input type="number" min="0" max="5" step="0.01" /></td>
          <td><input type="number" min="1" max="28" /></td>
          <td><button onclick="removeRow(this)">Remove</button></td>
        </tr>
      </tbody>
    </table>
    <button onclick="addCGPARow()">Add Trimester</button>
    <button onclick="calculateCGPA()">Calculate CGPA</button>
  </div>

  <div class="results" id="results"></div>

  <!-- Footer -->
  <footer>
    &copy; 2025 | Designed by Sualihu Mohammed
  </footer>

  <!-- Help Modal -->
  <div id="helpModal" class="modal">
    <div class="modal-content">
      <span class="close" onclick="closeHelp()">&times;</span>
      <h2>How to Use the GPA/CGPA Calculator</h2>
      <h3>GPA Calculation (Current Trimester):</h3>
      <ol>
        <li><strong>Select "GPA (Current Trimester Only)"</strong> from the dropdown</li>
        <li><strong>Add your courses:</strong> Click "Add Course" to enter all your courses</li>
        <li><strong>Enter details for each course:</strong>
          <ul>
            <li>Course Name (e.g., MATH101)</li>
            <li>Credit Hours (1-6)</li>
            <li>Your Score (0-100)</li>
          </ul>
        </li>
        <li><strong>Click "Calculate GPA"</strong> to see your trimester GPA</li>
      </ol>

      <h3>CGPA Calculation (Cumulative):</h3>
      <ol>
        <li><strong>Select "CGPA (Cumulative)"</strong> from the dropdown</li>
        <li><strong>Add your trimesters:</strong> Click "Add Trimester" for each completed trimester</li>
        <li><strong>Enter details for each trimester:</strong>
          <ul>
            <li>Trimester Name (e.g., L100 T1)</li>
            <li>GPA for that trimester (0-5.0)</li>
            <li>Total Credit Hours (1-28)</li>
          </ul>
        </li>
        <li><strong>Click "Calculate CGPA"</strong> to see your cumulative GPA and classification</li>
      </ol>

      <h3>Grading Scale:</h3>
      <table border="1" style="width: 100%; margin-bottom: 15px;">
        <tr>
          <th>Score Range</th>
          <th>Grade Point</th>
        </tr>
        <tr>
          <td>80-100</td>
          <td>5.0 (A+)</td>
        </tr>
        <tr>
          <td>75-79</td>
          <td>4.5 (A)</td>
        </tr>
        <tr>
          <td>70-74</td>
          <td>4.0 (B+)</td>
        </tr>
        <tr>
          <td>65-69</td>
          <td>3.5 (B)</td>
        </tr>
        <tr>
          <td>60-64</td>
          <td>3.0 (C+)</td>
        </tr>
        <tr>
          <td>55-59</td>
          <td>2.5 (C)</td>
        </tr>
        <tr>
          <td>50-54</td>
          <td>2.0 (D+)</td>
        </tr>
        <tr>
          <td>45-49</td>
          <td>1.5 (D)</td>
        </tr>
        <tr>
          <td>Below 45</td>
          <td>0.0 (F)</td>
        </tr>
      </table>

      <p><strong>Note:</strong> The classification (First Class, Second Class, etc.) is only shown for CGPA calculations.</p>
    </div>
  </div>

  <script>
    function scoreToGradePoint(score) {
      if (score >= 80) return 5.0;  // A+
      if (score >= 75) return 4.5;  // A
      if (score >= 70) return 4.0;  // B+
      if (score >= 65) return 3.5;  // B
      if (score >= 60) return 3.0;  // C+
      if (score >= 55) return 2.5;  // C
      if (score >= 50) return 2.0;  // D+
      if (score >= 45) return 1.5;  // D
      return 0.0;                  // F
    }

    function toggleMode() {
      const mode = document.getElementById("calcMode").value;
      document.getElementById("gpaSection").classList.toggle("hidden", mode !== "gpa");
      document.getElementById("cgpaSection").classList.toggle("hidden", mode !== "cgpa");
      document.getElementById("results").innerHTML = "";
    }

    function addRow() {
      const table = document.getElementById("courseTable").getElementsByTagName("tbody")[0];
      const newRow = table.rows[0].cloneNode(true);
      newRow.querySelectorAll("input").forEach(input => input.value = "");
      table.appendChild(newRow);
    }

    function addCGPARow() {
      const table = document.getElementById("cgpaTable").getElementsByTagName("tbody")[0];
      const newRow = table.rows[0].cloneNode(true);
      newRow.querySelectorAll("input").forEach(input => input.value = "");
      table.appendChild(newRow);
    }

    function removeRow(button) {
      const row = button.parentNode.parentNode;
      const table = row.parentNode;
      if (table.rows.length > 1) {
        table.removeChild(row);
      } else {
        alert("You must have at least one entry.");
      }
    }

    function calculateGPA() {
      const table = document.getElementById("courseTable").getElementsByTagName("tbody")[0];
      let totalCredits = 0;
      let totalPoints = 0;
      let hasError = false;

      for (let row of table.rows) {
        const courseName = row.cells[0].querySelector("input").value;
        const credit = parseFloat(row.cells[1].querySelector("input").value);
        const score = parseFloat(row.cells[2].querySelector("input").value);

        if (!courseName) {
          alert("Please enter a course name for all courses.");
          hasError = true;
          break;
        }

        if (isNaN(credit) || credit <= 0 || credit > 6) {
          alert("Please enter valid credit hours (1-6) for all courses.");
          hasError = true;
          break;
        }

        if (isNaN(score) || score < 0 || score > 100) {
          alert("Please enter valid scores (0-100) for all courses.");
          hasError = true;
          break;
        }

        const point = scoreToGradePoint(score);
        totalCredits += credit;
        totalPoints += point * credit;
      }

      if (hasError) return;

      const gpa = (totalPoints / totalCredits).toFixed(2);

      document.getElementById("results").innerHTML = `
        <h2>GPA Results:</h2>
        <p><span class="highlight">Total Credit Hours:</span> ${totalCredits}</p>
        <p><span class="highlight">GPA:</span> ${gpa}</p>
      `;
    }

    function calculateCGPA() {
      const table = document.getElementById("cgpaTable").getElementsByTagName("tbody")[0];
      let totalCredits = 0;
      let totalPoints = 0;
      let hasError = false;

      for (let row of table.rows) {
        const trimesterName = row.cells[0].querySelector("input").value;
        const gpa = parseFloat(row.cells[1].querySelector("input").value);
        const credit = parseFloat(row.cells[2].querySelector("input").value);

        if (!trimesterName) {
          alert("Please enter a trimester name for all entries.");
          hasError = true;
          break;
        }

        if (isNaN(gpa) || gpa < 0 || gpa > 5.0) {
          alert("Please enter valid GPA (0-5.0) for all trimesters.");
          hasError = true;
          break;
        }

        if (isNaN(credit) || credit <= 0 || credit > 28) {
          alert("Please enter valid credit hours (1-28) for all trimesters.");
          hasError = true;
          break;
        }

        totalCredits += credit;
        totalPoints += gpa * credit;
      }

      if (hasError) return;

      const cgpa = (totalPoints / totalCredits).toFixed(2);
      const classification = getClassification(cgpa);

      document.getElementById("results").innerHTML = `
        <h2>CGPA Results:</h2>
        <p><span class="highlight">Total Credit Hours:</span> ${totalCredits}</p>
        <p><span class="highlight">CGPA:</span> ${cgpa}</p>
        <p><span class="highlight">Classification:</span> ${classification}</p>
      `;
    }

    function getClassification(score) {
      const c = parseFloat(score);
      if (c >= 4.5) return "Honours - First Class";
      if (c >= 3.5) return "Honours - Second Class (Upper Division)";
      if (c >= 2.5) return "Honours - Second Class (Lower Division)";
      if (c >= 1.5) return "Honours - Third Class";
      return "Fail";
    }

    // Help Modal Functions
    function openHelp() {
      document.getElementById("helpModal").style.display = "block";
    }

    function closeHelp() {
      document.getElementById("helpModal").style.display = "none";
    }

    // Close modal when clicking outside of it
    window.onclick = function(event) {
      const modal = document.getElementById("helpModal");
      if (event.target == modal) {
        modal.style.display = "none";
      }
    }
  </script>

</body>
</html>
