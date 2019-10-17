# iOS
IOS documentation
# Http Request 
  - http request is made through **NSURLSession** object.
  - **NSURLSession** object has **NSURLSessionTask** object which performs and represents one `download` or `upload` task
  - **NSURLSessionTask** has various properties such as 
        1. `taskDescription` and `taskIdentifier`.
        2. `originalRequest` and `currentRequest`
        3. initial response from server
        4. countOfBytes
        5. `state` (.Running,. Susspended, .Canceling, .Completed)
        6. `error` if task is failed.
  - We can tell a task to `resume`, `suspend`, or `cancel`.
  - `task` is born `suspended` and won't start until we `resume` it.
  -  can change **NSURLSessionTask's** priority in `0 and 1` and it also provides three constants properties such as 
          - NSURLSessionTaskPriorityLow (0.25)
          - NSURLSessionTaskPriorityDefault (0.50)
          - NSURLSessionTaskPriorityHigh (0.75)
  - 4 kinds of session Task 
    1. `NSURLSessionDataTask`
    2. `NSURLSessionDownloadTask`
    3. `NSURLSessionUploadTask`
    4. `NSURLSessionStreamTask`
  - There are two ways to ask your **NSURLSession** for a new **NSURLSessionTask**:
    1. Call a **convenience** method
        The **convenience** methods all take a **completionHandler: parameter**. This com‐ pletion function is called when the task process ends. 
    2. Call a **delegate-based** method
        You give the NSURLSession a **delegate** when you create it, and the delegate is called back at various stages of a task’s progress.
  - Example 
    ``` 
    let s = "http://www.someserver.com/somefolder/someimage.jpg"
      let url = NSURL(string:s)!
      let session = NSURLSession.sharedSession()
      let task = session.downloadTaskWithURL(url) {
          (loc:NSURL?, response:NSURLResponse?, error:NSError?) in
          let d = NSData(contentsOfURL:loc!)!
          let im = UIImage(data:d)
          dispatch_async(dispatch_get_main_queue()) {
              self.iv.image = im
          }
      }
      task.resume()
      ```
