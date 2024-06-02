<script>
  // @ts-nocheck
  
    import { Router, Route } from "svelte-routing";
    import Home from "./pages/Home.svelte";
    import Login from "./pages/Login.svelte";
    import Register from "./pages/Register.svelte";
    // @ts-ignore
    import Cookies from "js-cookie";
    import axios from "axios";
    import Navbar from "./components/Navbar.svelte"
    import A4 from "./pages/404.svelte";
    import Logout from "./pages/Logout.svelte";
    import Footer from "./components/Footer.svelte";
    let Users;
    let user = Cookies.get("token");
    let pathname = "";
  
    async function GetData() {
      pathname = window.location.pathname;
      if (user) {
        try {
          const response = await axios.post(
            `http://localhost:3000/api/auth/user/`, {
              token: user
            }
          );
  
          if (response.data.status === "OK") {
            Users = response.data.data;
            console.log(response.data.data.token);
          } else {
            console.error("Kullanıcı hatası ?");
          }
        } catch (err) {
          console.error(err);
        }
      } else {
  
      }
    }
    GetData();
  
    export let url = "";
</script>
  
<main>
    <Router {url}>
     <Navbar users={Users}/>
      <div>
        <Route path="/"><Home users={Users} /></Route>
        <Route path="/login"><Login /></Route>
        <Route path="/register"><Register /></Route>
        {#if  Users}
        <Route path="/logout"><Logout /></Route>
        {/if}
        <Route path="*"><A4 /></Route>
      </div>
      <Footer />
    </Router>
</main>