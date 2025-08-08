### OWASP ZAP Scan Setup via GitHub Actions

#### Workflow Setup

1. **Create a GitHub Actions Workflow**  
   In your repository, navigate to `.github/workflows/`.  
   Create a new YAML file (e.g., `zap-scan.yml`).  

2. **Add the following workflow configuration:**  
   ```yaml  
   name: OWASP ZAP Scan  
   
   on:  
     push:  
       branches:  
         - main  
     pull_request:  
       branches:  
         - main  
   
   jobs:  
     zap:  
       runs-on: ubuntu-latest  
       steps:  
         - name: Checkout code  
           uses: actions/checkout@v2  

         - name: Run OWASP ZAP Scan  
           uses: zaproxy/action-full-scan@v0.1.0  
           with:  
             target: 'https://google-gruyere.appspot.com/'  
             format: 'json'  
             apiKey: ${{ secrets.ZAP_API_KEY }}  # Set your ZAP API key in GitHub secrets  
           
         - name: Upload scan report  
           uses: actions/upload-artifact@v2  
           with:  
             name: zap-scan-report  
             path: zap-report.json  
   ```

#### Execution Steps

1. **Trigger the GitHub Actions Workflow**  
   Push your changes to the `main` branch or create a pull request. This will automatically trigger the OWASP ZAP scan.

2. **Monitor the Workflow Execution**  
   Go to the "Actions" tab in your GitHub repository to see the progress of the workflow.

#### Retrieving the Scan Report Artifact

1. **Access the Artifacts**  
   Once the workflow completes, navigate to the specific workflow run in the "Actions" tab.

2. **Download the Report**  
   Look for the "zap-scan-report" artifact and download it for review.