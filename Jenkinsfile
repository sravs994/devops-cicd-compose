peline {
    agent any

        stages {

	        stage('Checkout') {
		            steps {
			                    checkout scm
					                }
							        }

								        stage('Build Info') {
									            steps {
										                    echo "Branch: ${env.BRANCH_NAME}"
												                    echo "Build Number: ${env.BUILD_NUMBER}"
														                }
																        }

																	        stage('Unit Tests') {
																		            steps {
																			                    echo "Running unit tests (placeholder)"
																					                }
																							        }

																								    }

																								        post {
																									        always {
																										            echo "Pipeline finished for ${env.BRANCH_NAME}"
																											            }
																												        }
																													}

