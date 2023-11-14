<script>
    import "../app.css";
	import { isLoggedIn } from "../utils/auth";
    function headerLogIn(){}
  </script>





<div class = "header" style = padding:1.5em> 
    <div class = "float-right flex flex-row gap-2"> 
        <div class = "login"> 
        {#if $isLoggedIn}
          <a href="/users/login" class="text-white bg-transparent-700 hover:bg-gray-300 hover:text-yellow-950 focus:ring-4 focus:ring-transparent-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-transparent-600 dark:hover:bg-transparent-700 focus:outline-none dark:focus:ring-transparent-800">Log Out </a>
        
          {:else}
          <a href="/users/login" class="text-white bg-transparent-700 hover:bg-gray-300 hover:text-yellow-950 focus:ring-4 focus:ring-transparent-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-transparent-600 dark:hover:bg-transparent-700 focus:outline-none dark:focus:ring-transparent-800">Log In</a>
        
          {/if}
        </div>
        <div>
            <a href="/jobs/create" class="text-white bg-transparent-700 hover:bg-gray-300 hover:text-yellow-950 focus:ring-4 focus:ring-transparent-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-transparent-600 dark:hover:bg-transparent-700 focus:outline-none dark:focus:ring-transparent-800"> Post A Job  </a>
        </div>
    </div>

    <div class = "left" style = float:left>
        <a href="/" class="font-bold text-white bg-transparent-900 hover:bg-transparent-800 focus:ring-4 focus:ring-transparent-300 font-large rounded-lg text-2xl px-5 py-2.5 mr-2 mb-2 dark:bg-transparent-600 dark:hover:bg-grey-700 focus:outline-none dark:focus:ring-transparent-800">NEXT Jobs</a>
        
    </div>
</div>
