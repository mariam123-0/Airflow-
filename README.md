# Airflow
This Airflow DAG is designed to demonstrate the basic functionality of task execution and dependency management in Apache Airflow. It consists of three simple tasks: the first task prints the current date to indicate when the workflow is executed, the second task displays a welcome message with the user’s name to confirm that the pipeline is running successfully, and the third task generates a random number and saves it to a file for later use. Together, these tasks provide a clear example of how Airflow can be used to automate and organize sequential operations in a workflow.

# code

    from airflow import DAG
    from airflow.operators.bash import BashOperator
    from airflow.operators.python import PythonOperator
    from datetime import datetim
    import random
    
    with DAG("Airflow_Depi", 
        start_date=datetime(2025, 10, 1),
        schedule_interval=None, 
        catchup=False) as dag:

    t1 = BashOperator(
        task_id="print_date",
        bash_command="date")

    t2 = PythonOperator(
        task_id="print_welcome",
        python_callable=lambda: print("Hello this is Mariam!"))

    t3 = PythonOperator(
        task_id="generate_number",
        python_callable=lambda: open("/tmp/random.txt", "w").write(str(random.randint(1, 100))))

    t1 >> t2 >> t3
