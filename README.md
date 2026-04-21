<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>mysh - A Custom Unix Shell</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
            background-color: #0d1117;
            color: #c9d1d9;
            line-height: 1.6;
            padding: 40px 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        h1 {
            font-size: 2em;
            font-weight: 600;
            color: #f0f6fc;
            margin-bottom: 16px;
            border-bottom: 1px solid #30363d;
            padding-bottom: 16px;
        }

        h2 {
            font-size: 1.5em;
            font-weight: 600;
            color: #f0f6fc;
            margin-top: 32px;
            margin-bottom: 16px;
            border-bottom: 1px solid #30363d;
            padding-bottom: 8px;
        }

        h3 {
            font-size: 1.1em;
            font-weight: 600;
            color: #f0f6fc;
            margin-top: 24px;
            margin-bottom: 12px;
        }

        p {
            margin-bottom: 16px;
            color: #c9d1d9;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 24px;
            border: 1px solid #30363d;
        }

        th {
            background-color: #0d1117;
            color: #f0f6fc;
            padding: 12px 16px;
            text-align: left;
            font-weight: 600;
            border: 1px solid #30363d;
        }

        td {
            padding: 12px 16px;
            border: 1px solid #30363d;
            background-color: #0d1117;
        }

        tr:hover {
            background-color: #161b22;
        }

        code {
            background-color: #161b22;
            color: #79c0ff;
            padding: 0.2em 0.4em;
            border-radius: 6px;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
        }

        pre {
            background-color: #161b22;
            border: 1px solid #30363d;
            border-radius: 6px;
            padding: 16px;
            overflow-x: auto;
            margin-bottom: 24px;
            color: #c9d1d9;
        }

        pre code {
            background: none;
            color: #c9d1d9;
            padding: 0;
            border-radius: 0;
        }

        .bash {
            color: #79c0ff;
        }

        .comment {
            color: #8b949e;
        }

        ul, ol {
            margin-left: 20px;
            margin-bottom: 16px;
        }

        li {
            margin-bottom: 8px;
        }

        a {
            color: #58a6ff;
            text-decoration: none;
        }

        a:hover {
            text-decoration: underline;
        }

        .intro {
            font-size: 1.1em;
            color: #c9d1d9;
            margin-bottom: 32px;
            line-height: 1.8;
        }

        .section-divider {
            margin-top: 40px;
        }

        .footer {
            margin-top: 40px;
            padding-top: 16px;
            border-top: 1px solid #30363d;
            color: #8b949e;
            font-size: 0.9em;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>mysh - A Custom Unix Shell</h1>
        
        <p class="intro">A feature-rich Unix shell in C with built-in commands, variables, pipes, background processes, and TCP chat.</p>

        <h2>Built-in Commands</h2>
        
        <table>
            <thead>
                <tr>
                    <th>Command</th>
                    <th>Usage</th>
                    <th>Description</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><code>echo</code></td>
                    <td><code>echo [args...]</code></td>
                    <td>Print arguments separated by spaces</td>
                </tr>
                <tr>
                    <td><code>cd</code></td>
                    <td><code>cd &lt;path&gt;</code></td>
                    <td>Change directory (supports <code>.</code>, <code>..</code>, relative, absolute)</td>
                </tr>
                <tr>
                    <td><code>ls</code></td>
                    <td><code>ls [path] [--rec] [--d &lt;depth&gt;] [--f &lt;substring&gt;]</code></td>
                    <td>List directory contents with optional recursion, depth limit, and filtering</td>
                </tr>
                <tr>
                    <td><code>cat</code></td>
                    <td><code>cat [file]</code></td>
                    <td>Display file contents or read stdin</td>
                </tr>
                <tr>
                    <td><code>wc</code></td>
                    <td><code>wc [file]</code></td>
                    <td>Count words, characters, and lines</td>
                </tr>
                <tr>
                    <td><code>ps</code></td>
                    <td><code>ps</code></td>
                    <td>List background processes</td>
                </tr>
                <tr>
                    <td><code>kill</code></td>
                    <td><code>kill &lt;pid&gt; [signal]</code></td>
                    <td>Kill a process (default: SIGTERM)</td>
                </tr>
                <tr>
                    <td><code>exit</code></td>
                    <td><code>exit</code></td>
                    <td>Exit the shell</td>
                </tr>
            </tbody>
        </table>

        <h2>Shell Variables</h2>
        
        <p>Define variables with <code>var=value</code> and expand with <code>$var</code>:</p>
        
        <pre><code>mysh$ greeting=hello
mysh$ echo $greeting
hello</code></pre>

        <h2>Pipes</h2>
        
        <p>Chain commands with <code>|</code>:</p>
        
        <pre><code>mysh$ cat file.txt | wc
mysh$ echo hello | cat</code></pre>

        <h2>Background Processes</h2>
        
        <p>Run commands with <code>&amp;</code>:</p>
        
        <pre><code>mysh$ long_running_command &amp;
[1] 12345</code></pre>

        <p>Returns immediately to the prompt.</p>

        <h2>TCP Chat System</h2>
        
        <table>
            <thead>
                <tr>
                    <th>Command</th>
                    <th>Usage</th>
                    <th>Description</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><code>start-server</code></td>
                    <td><code>start-server &lt;port&gt;</code></td>
                    <td>Start a chat server</td>
                </tr>
                <tr>
                    <td><code>close-server</code></td>
                    <td><code>close-server</code></td>
                    <td>Shut down the server</td>
                </tr>
                <tr>
                    <td><code>start-client</code></td>
                    <td><code>start-client &lt;port&gt; &lt;host&gt;</code></td>
                    <td>Connect as a client</td>
                </tr>
                <tr>
                    <td><code>send</code></td>
                    <td><code>send &lt;port&gt; &lt;host&gt; &lt;message&gt;</code></td>
                    <td>Send a one-off message</td>
                </tr>
            </tbody>
        </table>

        <p>In client mode, type <code>\connected</code> to see active connections.</p>

        <h2>Build &amp; Run</h2>
        
        <pre><code>make              <span class="comment"># Compile</span>
make clean        <span class="comment"># Clean artifacts</span>
./mysh            <span class="comment"># Run</span></code></pre>

        <h2>Signal Handling</h2>
        
        <table>
            <thead>
                <tr>
                    <th>Signal</th>
                    <th>Behavior</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><code>Ctrl+C</code></td>
                    <td>Redisplay prompt (don't exit)</td>
                </tr>
                <tr>
                    <td><code>Ctrl+D</code></td>
                    <td>Exit gracefully</td>
                </tr>
                <tr>
                    <td><code>SIGTERM/SIGHUP</code></td>
                    <td>Clean shutdown with server cleanup</td>
                </tr>
                <tr>
                    <td><code>SIGCHLD</code></td>
                    <td>Auto-reap background processes</td>
                </tr>
            </tbody>
        </table>

        <h2>ls Options</h2>
        
        <pre><code>mysh$ ls                        <span class="comment"># Current directory</span>
mysh$ ls /home                  <span class="comment"># Specific directory</span>
mysh$ ls --rec                  <span class="comment"># Recursive (unlimited depth)</span>
mysh$ ls --rec --d 2            <span class="comment"># Recursive with max depth 2</span>
mysh$ ls --f .txt               <span class="comment"># Filter files by substring</span>
mysh$ ls --rec --d 3 --f test   <span class="comment"># Combine options</span></code></pre>

        <h2>Project Structure</h2>
        
        <pre><code>├── mysh.c              <span class="comment"># Main shell loop</span>
├── builtins.c/h        <span class="comment"># Built-in commands</span>
├── commands.c/h        <span class="comment"># Server/client commands</span>
├── client_manager.c/h  <span class="comment"># TCP socket management</span>
├── variables.c/h       <span class="comment"># Variable storage &amp; expansion</span>
├── io_helpers.c/h      <span class="comment"># I/O utilities &amp; tokenization</span>
└── Makefile</code></pre>

        <h2>Limits</h2>
        
        <ul>
            <li>Input line: 128 chars max</li>
            <li>Chat username: 10 chars max</li>
            <li>Chat message: 129 chars max</li>
            <li>Background processes: Up to 1000 PIDs</li>
        </ul>

        <h2>Requirements</h2>
        
        <ul>
            <li>GCC</li>
            <li>POSIX system (Linux/macOS)</li>
            <li>Standard C libraries</li>
        </ul>

        <h2>License</h2>
        
        <p>Educational purposes.</p>

        <div class="footer">
            <p>© 2024 mysh Project. All rights reserved.</p>
        </div>
    </div>
</body>
</html>
