<!-- shared with plugins that use queues: http-log, datadog, statsd, opentelemetry -->
    - name: name
      type: string
      description: name of the queue
    - name: batch_max_size
      type: number
      default: 1
      description: maximum number of entries to be given to the handler as a batch"
    - name: max_delay
      type: number
      default: 1
      description: maximum number of (fractional) seconds to elapse after the first entry was queued before the queue starts calling the handler
    - name: capacity
      type: number
      default: 10000
      description: maximum number of entries that can be waiting on the queue
    - name: string_capacity
      type: number
      default: nil
      description: maximum number of bytes that can be waiting on a queue, requires string content
    - name: max_retry_time
      type: number
      default: 60
      description: time in seconds before the queue gives up calling a failed handler for a batch
    - name: max_retry_delay
      type: number
      default: 60
      description: maximum time in seconds between retries, caps exponential backoff"
    - name: poll_time
      type: number
      default: 1
      description: time in seconds between polls for worker shutdown
    - name: max_idle_time
      type: number
      default: 60
      description: time in seconds before an idle queue is deleted
