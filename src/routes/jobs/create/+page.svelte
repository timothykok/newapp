<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    import { authenticateUser } from '../../../utils/auth.js';
    let formErrors = {};


  
    export function navigateJob() {
        const jobIdSlug = slugify(userData.title);
        goto('/jobs/new');
    }


    export async function createJob(evt) {
      evt.preventDefault()

      const userData = {
        title: evt.target['jobtitle'].value,
        minAnnualCompensation: evt.target['minAnnualCompensation'].value,
        maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
        description: evt.target['description'].value,
        requirements: evt.target['requirements'].value,
        employer: evt.target['employer'].value,
        location: evt.target['location'].value,
        applicationInstructions: evt.target['applicationInstructions'].value,
        user: getUserId()
      };
      
      const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/users/records', {
        method: 'POST',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(userData)
      });
  
      if (resp.status == 200) {
        const res = await authenticateUser(userData.username, userData.password);
  
        if (res.success) {
          navigateJob(); //to change 
        } else {
          throw 'Job created succeeded but authentication failed :(';
        }

        
      } else {
        const res = await resp.json();
        formErrors = res.data;
        goto("/users/login");  
      }
    }
  </script>
  

  <div class= "p-14" >
    <h1 class="text-left text-3xl">Post A Job</h1>
    <div class="text-left">
        <p> Find Your Next Hire Here</p>
    </div>
    <div class="flex justify-left items-center mt-8 h-full pr-64 pb-7">
        <form on:submit={createJob} class="w-full">
            <div class="form-control w-full">
              <label class="label" for="title">
                  <span class="label-text">Job Title</span>
              </label>
              <input type="text" name="jobtitle" placeholder="Software Engineer" class="input input-bordered w-full" required />
              {#if 'title' in formErrors}
              <label class="label" for="title">
                  <span class="label-text-alt text-red-500">{formErrors['jobtitle'].message}</span>
              </label>
              {/if}
          </div>

          <div class="form-control w-full">
            <label class="range" for="minAnnualCompensation">
                <span class="label-text"> Minimum Compensation Range </span>
            </label>
            <input type="range" min="0" max="100" value="25" class="range" step="25" />
                <div class="w-full flex justify-between text-xs px-2">
                  <span>3,000</span>
                  <span>6,000</span>
                  <span>9,000</span>
                  <span>12,000</span>
                  <span>15,000</span>
                </div>
            {#if 'minAnnualCompensation' in formErrors}
            <label class="label" for="minAnnualCompensation">
                <span class="label-text-alt text-red-500">{formErrors['minAnnualCompensation'].message}</span>
            </label>
            {/if}
        </div>



    
            <div class="form-control w-full">
                <label class="range" for="maxAnnualCompensation">
                    <span class="label-text"> Max Compensation Range </span>
                </label>
                <input type="range" min="0" max="100" value="25" class="range" step="25" />
                    <div class="w-full flex justify-between text-xs px-2">
                      <span>3,000</span>
                      <span>6,000</span>
                      <span>9,000</span>
                      <span>12,000</span>
                      <span>15,000</span>
                    </div>
                {#if 'maxAnnualCompensation' in formErrors}
                <label class="label" for="maxAnnualCompensation">
                    <span class="label-text-alt text-red-500">{formErrors['vol'].message}</span>
                </label>
                {/if}
            </div>
  

            <div class="form-control w-full">
              <label class="label" for="employer">
                  <span class="label-text">Company Name</span>
              </label>
              <input type="text" name="employer" placeholder="e.g. Facebook" class="input input-bordered w-full" required />
              {#if 'employer' in formErrors}
              <label class="text" for="employer">
                  <span class="label-text-alt text-red-500">{formErrors['employer'].message}</span>
              </label>
              {/if}
            </div>

            <div class="form-control w-full">
              <label class="label" for="location">
                  <span class="label-text">Job Location</span>
              </label>
              <input type="text" name="location" placeholder="e.g. Singapore" class="input input-bordered w-full" required />
              {#if 'location' in formErrors}
              <label class="text" for="location">
                  <span class="label-text-alt text-red-500">{formErrors['email'].message}</span>
              </label>
              {/if}
            </div>

            <div class="form-control w-full">
              <label class="text" for="description">
                  <span class="label-text">Description</span>
              </label>
              <input type="text" name="description" class="input input-bordered w-full h-60 align-text-top" required />
              {#if 'description' in formErrors}
              <label class="text" for="description">
                  <span class="label-text-alt text-red-500">{formErrors['Description'].message}</span>
              </label>
              {/if}
            </div>

            <div class="form-control w-full">
              <label class="text" for="requirements">
                  <span class="label-text">Requirements</span>
              </label>
              <input type="text" name="requirements"  class="input input-bordered w-full h-40 align-text-top" required />
              {#if 'requirements' in formErrors}
              <label class="text" for="requirements">
                  <span class="label-text-alt text-red-500">{formErrors['requirements'].message}</span>
              </label>
              {/if}
            </div>

            <div class="form-control w-full">
              <label class="text" for="applicationInstructions">
                  <span class="label-text">Application Instructions</span>
              </label>
              <input type="text" name=" applicationInstructions" class="input input-bordered w-full h-20" required />
              {#if 'location' in formErrors}
              <label class="text" for=" applicationInstructions">
                  <span class="label-text-alt text-red-500">{formErrors['applicationInstructions'].message}</span>
              </label>
              {/if}
            </div>
    
            <div class="form-control w-64 mt-4 float-right">
              <button on:click = {navigateJob} class="btn btn-neutral" >Post Job</button>

              
              
            
            </div>
        </form>
    </div>
</div>