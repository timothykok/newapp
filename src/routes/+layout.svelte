<script>
    import "../app.css";
	  import { isLoggedIn } from "../utils/auth";
    import Header from '../components/Header.svelte'
    import { Alert } from "../components/Alert.svelte";

  </script>


  

<Header />
<slot />
