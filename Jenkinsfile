pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run TestHub Suite') {
            steps {
                writeFile file: 'payload.json', text: '''
{
  "offlineToken": "YOUR_OFFLINE_TOKEN",
  "testAsset": {
    "assetId": "523037cda6b0963561fe038468175aab5c3203723ea9a9fdead4ac77e184bf98",
    "revision": "Boat-UI-Design"
  }
}
'''

                bat '''
curl -k -X POST "https://devopsautomation.hcl-software.com/test/rest/projects/6350/executions/" ^
-H "Authorization: Bearer YOUR_ACCESS_TOKEN" ^
-H "Content-Type: application/json" ^
-H "accept-version: 1.4" ^
-d @payload.json ^
-o response.json ^
-w "HTTP_STATUS:%%{http_code}"

echo Response:
type response.json
'''
            }
        }
    }
}
