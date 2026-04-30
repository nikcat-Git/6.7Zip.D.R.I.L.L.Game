pipeline {
    agent any
    
    parameters {
        choice(name: 'STUDENT_NAME', choices: ['Yevhenii', 'Denis', 'Artem', 'Mykhailo', 'Serhii'], description: 'Оберіть своє ім’я')
        choice(name: 'TEST_SET', choices: ['Set_1_Quality', 'Set_2_Security', 'Set_3_Structure', 'Set_4_Performance', 'Set_5_Deps'], description: 'Оберіть свій набір тестів')
    }

    tools {
        nodejs 'node-latest' 
    }

    stages {
        stage('Install') {
            steps {
                echo "Студент ${params.STUDENT_NAME} розпочинає підготовку..."
                bat 'npm install'
            }
        }

        stage('Testing') {
            steps {
                script {
                    switch(params.TEST_SET) {
                        case 'Set_1_Quality':
                            echo "Тести Євгенія: Якість коду"
                            bat 'npm run lint'
                            bat 'npx tsc --noEmit'
                            bat 'npm run build'
                            break
                            
                        case 'Set_2_Security':
                            echo "Тести Набору 2: Безпека"
                            bat 'npm audit'
                            bat 'if exist package-lock.json echo Lock_File_Present'
                            bat 'npm outdated'
                            break
                            
                        case 'Set_3_Structure':
                            echo "Тести Набору 3: Структура проекту"
                            bat 'if exist next.config.ts echo NextConfig_OK'
                            bat 'if exist .gitignore echo Git_Rules_Present'
                            bat 'if exist app\\page.tsx echo Main_Page_Exists'
                            break

                        case 'Set_4_Performance':
                            echo "Тести Набору 4: Продуктивність"
                            bat 'npm run build'
                            bat 'echo Перевірка розміру папки .next'
                            bat 'dir .next /s'
                            bat 'echo Аналіз завершено'
                            break

                        case 'Set_5_Deps':
                            echo "Тести Набору 5: Залежності"
                            bat 'npm list --depth=0'
                            bat 'npm audit --audit-level=high'
                            bat 'echo Перевірка конфігурації Node'
                            bat 'node -v'
                            break
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Звіт сформовано для: ${params.STUDENT_NAME}. Результат тестування дивіться у Stage View."
        }
    }
}