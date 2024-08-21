<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Construction Estimation Tool</title>
    <style>
        body {
            font-family: Helvetica, Arial, sans-serif;
            background-color: #f9f9f9;
            margin: 0;
            padding: 20px;
            color: #333;
        }

        header {
            background-color: #005b99;
            color: white;
            text-align: center;
            padding: 20px 0;
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }

        .container {
            max-width: 1200px;
            margin: 20px auto;
            background-color: white;
            padding: 30px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }

        h1, h2, h3 {
            color: #333;
            margin-bottom: 10px;
            font-weight: normal;
        }

        h2 {
            border-bottom: 2px solid #e6e6e6;
            padding-bottom: 10px;
            margin-bottom: 20px;
        }

        .section {
            margin-bottom: 40px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            font-size: 14px;
            color: #555;
        }

        th, td {
            padding: 12px;
            border: 1px solid #e6e6e6;
            text-align: left;
        }

        th {
            background-color: #007acc;
            color: white;
            font-weight: bold;
        }

        input[type="text"], input[type="number"], input[type="email"], input[type="date"] {
            width: 100%;
            padding: 10px;
            border-radius: 4px;
            border: 1px solid #ccc;
            box-sizing: border-box;
            font-size: 14px;
            color: #333;
        }

        button {
            background-color: #007acc;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
            margin-top: 20px;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #005b99;
        }

        .summarySection {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
        }

        .pdf-section {
            margin-top: 40px;
            text-align: center;
        }

        .total-summary {
            font-size: 16px;
            font-weight: bold;
            color: #005b99;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1>Construction Estimation Tool</h1>
        </div>
    </header>

    <div class="container">
        <!-- Company Information Section -->
        <div class="section">
            <h2>Company Information</h2>
            <div class="address-container">
                <div>
                    <label for="companyName">Company Name:</label>
                    <input type="text" id="companyName" placeholder="Enter company name" />
                </div>
                <div>
                    <label for="companyAddress">Company Address:</label>
                    <input type="text" id="companyAddress" placeholder="Enter company address" />
                </div>
            </div>
            <div class="address-container">
                <div>
                    <label for="companyEmail">Company Email:</label>
                    <input type="email" id="companyEmail" placeholder="Enter company email" />
                </div>
                <div>
                    <label for="companyPhone">Company Phone:</label>
                    <input type="text" id="companyPhone" placeholder="Enter company phone number" />
                </div>
            </div>
        </div>

        <!-- Client Information Section -->
        <div class="section">
            <h2>Client Information</h2>
            <div class="address-container">
                <div>
                    <label for="clientName">Client Name:</label>
                    <input type="text" id="clientName" placeholder="Enter client name" />
                </div>
                <div>
                    <label for="clientAddress">Client Address:</label>
                    <input type="text" id="clientAddress" placeholder="Enter client address" />
                </div>
            </div>
            <div class="address-container">
                <div>
                    <label for="clientEmail">Client Email:</label>
                    <input type="email" id="clientEmail" placeholder="Enter client email" />
                </div>
                <div>
                    <label for="clientPhone">Client Phone:</label>
                    <input type="text" id="clientPhone" placeholder="Enter client phone number" />
                </div>
            </div>
        </div>

        <!-- Project Details Section -->
        <div class="section">
            <h2>Project Details</h2>
            <div class="address-container">
                <div>
                    <label for="projectName">Project Name:</label>
                    <input type="text" id="projectName" placeholder="Enter project name" />
                </div>
                <div>
                    <label for="projectDate">Project Start Date:</label>
                    <input type="date" id="projectDate" />
                </div>
            </div>
            <label for="projectDescription">Project Description:</label>
            <input type="text" id="projectDescription" placeholder="Enter a brief project description" />
        </div>

        <!-- Construction Details Section -->
        <div class="section">
            <h2>Construction Estimation Details</h2>
            <table id="estimationTable">
                <thead>
                    <tr>
                        <th>Description</th>
                        <th>Detail</th>
                        <th>Material Cost per Unit</th>
                        <th>Quantity</th>
                        <th>Labor Cost per Hour</th>
                        <th>Labor Hours</th>
                        <th>Total Material Cost</th>
                        <th>Total Labor Cost</th>
                        <th>Total Cost</th>
                    </tr>
                </thead>
                <tbody id="estimationTableBody">
                    <!-- Rows will be dynamically added here -->
                </tbody>
            </table>
            <button onclick="addRow()">+ Add Construction Detail</button>
        </div>

        <!-- Suppliers Section -->
        <div class="section">
            <h2>Supplier Information</h2>
            <table id="supplierTable">
                <thead>
                    <tr>
                        <th>Use</th>
                        <th>Material</th>
                        <th>Supplier</th>
                        <th>Quote Details</th>
                    </tr>
                </thead>
                <tbody id="supplierTableBody">
                    <!-- Rows will be dynamically added here -->
                </tbody>
            </table>
            <button onclick="addSupplier()">+ Add Supplier</button>
        </div>

        <!-- Summary Section -->
        <div class="section">
            <h2>Summary</h2>
            <div id="summarySection" class="result">
                <div class="summarySection">
                    <h3>Total Labor Cost:</h3> 
                    <h3 id="summaryLaborCost">0</h3>
                </div>
                <div class="summarySection">
                    <h3>Total Material Cost:</h3> 
                    <h3 id="summaryMaterialCost">0</h3>
                </div>
                <div class="summarySection">
                    <h3>Total Cost:</h3> 
                    <h3 id="summaryTotalCost">0</h3>
                </div>
            </div>
        </div>

        <!-- Tax and Markup Section -->
        <div class="section">
            <h2>Tax and Markup</h2>
            <div class="address-container">
                <div>
                    <label for="taxRate">Tax Rate (%):</label>
                    <input type="number" id="taxRate" value="10" onchange="updateTotal()">
                </div>
                <div>
                    <label for="markupRate">Markup Rate (%):</label>
                    <input type="number" id="markupRate" value="15" onchange="updateTotal()">
                </div>
            </div>
            <div id="totalWithTaxAndMarkup" class="result">
                <div class="summarySection">
                    <h3>Total with Tax and Markup:</h3>
                    <h3 id="finalTotalCost">0</h3>
                </div>
            </div>
        </div>

        <!-- PDF Generation Section -->
        <div class="pdf-section">
            <h2>Generate PDF</h2>
            <button onclick="generateClientPDF()">Download Client Copy (Lump Sum)</button>
            <button onclick="generateInternalPDF()">Download Internal Copy (Detailed)</
