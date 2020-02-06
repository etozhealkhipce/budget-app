<template>
  <el-card class="form-card">
    <el-form :model="formData" ref="addItemForm" :rules="rules" label-position="left">
      <el-form-item label="Type" prop="type">
        <el-select class="type-select" v-model="formData.type" placeholder="Choose type...">
          <el-option label="Income" value="INCOME"></el-option>
          <el-option label="Outcome" value="OUTCOME"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="Comments" prop="comment">
        <el-input v-model="formData.comment" placeholder="Input comment"/>
      </el-form-item>
      <el-form-item label="Value" prop="value">
        <el-input v-model.number="formData.value" placeholder="Input value"/>
      </el-form-item>
      <el-button type="primary" @click="onSubmit">Submit</el-button>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name: 'Form',
  data: () => ({
    formData: {
      type: "",
      comment: '',
      value: null,
    },
    rules: {
      type: [{ required: true, message: "Please choose type", trigger: "blur" }],
      comment: [{ required: true, message: "Please input comment", trigger: "change"}],
      value: [{ required: true, message: "Please input comment", trigger: "change"},
              { type: "number", message: "Value must be a number", trigger: "change"}]

    },
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          this.$emit("submitForm", { ...this.formData });
          this.$refs.addItemForm.resetFields();
        }
      });
    }
  },

}
</script>

<style scoped>
.form-card {
  max-width: 40%;
  margin: auto;
}

.type-select {
  width: 100%;
}
</style>