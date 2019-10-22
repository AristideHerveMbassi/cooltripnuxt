<template>
  <div>
    <b-alert
      show
      variant="success"
    >
      You should see this page without need to authentication!
    </b-alert>

    <div>
      <b-jumbotron class="text-center" header="Partners" lead="Add new partners">
        <p>Please the form with the phone number of the user and click on the button to add them into partners area</p>
      </b-jumbotron>
    </div>
    <add-partners></add-partners>
  </div>
</template>

<script>
import AddPartners from '../../../components/Adminstration/Partners/AddPartners'
export default {
  name: 'Add',
  components: {
    AddPartners
  }
}
</script>

<style scoped>

</style>
