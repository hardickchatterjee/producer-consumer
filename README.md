# producer-consumer
Producer consumer thread functions for Project 2


Function for the producer thread

int producer_thread_function(void *pv)
{
	allow_signal(SIGKILL);
	struct task_struct *task;

	for_each_process(task)
	{
		if (task->cred->uid.val == uuid)
		{
			// TODO Implement your producer kernel thread here
			// use kthread_should_stop() to check if the kernel thread should stop
			// use down() and up() for semaphores
			// Hint: Please refer to sample code to see how to use process_info struct
			// Hint: kthread_should_stop() should be checked after down() and before up()
      // we will search the system for processes with the same uid as the one passed in
      // we will then add the process to the buffer


      if (fill < MAX_BUFFER_SIZE) {
        down(&empty);
        down(&mutex);

        if (kthread_should_stop()) {
          up(&mutex);
          up(&empty);
          break;
        }

        buffer[fill].pid = task->pid;
        buffer[fill].start_time = task->start_time;
        fill++;

        if (kthread_should_stop()) {
          up(&mutex);
          up(&empty);
          break;
        }

        up(&mutex);
        up(&full);
      }


			total_no_of_process_produced++;
			PCINFO("[%s] Produce-Item#:%d at buffer index: %d for PID:%d \n", current->comm,
				   total_no_of_process_produced, (fill + buffSize - 1) % buffSize, task->pid);
		}
	}
 }

	PCINFO("[%s] Producer Thread stopped.\n", current->comm);
	ctx_producer_thread[0] = NULL;
	return 0;
