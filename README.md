# project1-cs3700

<h3> High-level approach </h3>
<p>
  1. Get commandline arguments, parse into variables
  2. Make connection to server and get welcome message. Send USER. Send PASS if there is one
  3. If the command is simple and doesn't need a passive connection, simply do it and quit
  4. If the command requires a passive connection, create it
  5. If the command requires you to differentiate between URLS (i.e. mv needs to know if local or ftp
      comes first), make sure to figure out where the file is going and deal with it based on that
      information. Send the data and quit.
  6. If the command just requires a passive channel but no two-url logic, just use the passive channel
      and send the data. Then quit.
</p>
<h3> Challenges </h3>
<p>
  My number one challenge in this project was not really knowing how FTP actually worked. I had to
  read over the project description several times to get a good idea of what exactly I had to do.
  The biggest issue I had was with file upload and download, because I wasn't quite sure as to
  how to send the file or when to send it, so I had to look all of these things up and do a lot of
  testing to make sure that what I was doing was correct.
  Another challenge I had was how I should separate my code. When I was getting into PASV functionality,
  I realized that most of my code was just in a single method, so I had to think of ways to delegate
  the jobs so that I wouldn't have spaghetti code. I ended up separating it by grouping up the functions
  and then delegating the responsibilities to other methods if the function was more complex. For example,
  mkdir is easy and doesn't require a passive channel, but ls does. mv is more complex than ls because
  it requires you to make sure you know if the file is moving from local to ftp or ftp to local.
  As a result, these were all in separate methods.
</p>
<h3> Testing strategy </h3>
<p>
  I employed a lot of print testing. Whenever I ran into issues or wanted to see if what I wrote was working, 
    I printed out in the console what I was doing. Examples:
  1. When handling the passive channel IP parsing, I had to print a lot to make sure I was parsing
      out the IP correctly because I had to do a lot of substringing and replacing
  2. Printing what the FTP server replies to me. Either it gave me a good response or it told me what
      I had to fix; for example, at one point I was messing up when to upload a file so I realized that
      the server sends an "Ok to upload" and then I upload it.
  3. When I was parsing out the FTP url data, I needed to make sure I was getting the right 
      url attributes so I printed out what I was receiving for that as well.

  I also did a lot of manual testing. This went especially for mv, cp, and ls -- I made sure to 
    try to mv and cp files to and from the server and then ls to see if it worked, as well as cat
    the file contents to ensure nothing was lost (or gained ..?) along the way.
    ls was very helpful to make sure that the functions were in fact working on the server.


  I tested a few times against the server itself. I only actually had two issues with my code when
    I submitted: I first realized that the way I was parsing ip's didn't work for the submission
    tests. After I printed the ftp PASV response, I realized that the submission tests were different
    in the fact that there was a period at the end of the IP that I wasn't ready for, so I had to
    patch that.
  The other issue I had was that file transfers were occasionally erroring due to some weird byte issue.
    I looked up the error and realized I needed to open the files in bit mode, and that fixed my issue.
</p>
