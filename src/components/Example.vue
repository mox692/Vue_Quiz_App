<template>
<div>
    <b-form-checkbox
      id="checkbox-1"
      v-model="status"
      name="checkbox-1"
      value="accepted"
      unchecked-value="not_accepted"
    >
      I accept the terms and use
    </b-form-checkbox>

    <div>State: <strong>{{ status }}</strong></div>
</div>

</template>

<style scoped>
p {
  font-size: 30px;
}

</style>