CREATE FUNCTION validate_nui_length()
RETURNS TRIGGER AS $$
BEGIN
  -- Verificar que el NUI tenga exactamente 10 caracteres
  IF LENGTH(NEW.nui) != 10 THEN
    RAISE EXCEPTION 'El campo nui debe tener exactamente 10 caracteres.';
  END IF;

  -- Verificar que cada carácter en el NUI sea numérico
  IF NEW.nui ~ '[^0-9]' THEN
    RAISE EXCEPTION 'El campo nui debe contener solo caracteres numéricos.';
  END IF;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

![cap1] capturas/cap1.png